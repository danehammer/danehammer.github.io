---

title:  "Rock, Paper, Scissors, Go!"
categories: programming
---

When `core.async` was new and I was kinda learning Clojure, I bookmarked Alex Miller's [blog post][alex] about implementing Rock, Paper, Scissors with channels. So now I've done the same in Go.

Here's what I did and what I was thinking.

```go
type move string

const (
	rock     move = "rock"
	paper    move = "paper"
	scissors move = "scissors"
)

var moves = [3]move{rock, paper, scissors}
```

I made a type for the moves, and a var for all of them, so I could make random moves:

```go
import "math/rand"

move := rand.Intn(len(moves))
```

Then added a function that makes an unbuffered channel that produces random moves.

```go
type play struct {
	move move
	name string
}

func makePlayer(name string) <-chan play {
	out := make(chan play)
	go func() {
		for { // ever
			i := rand.Intn(len(moves))
			out <- play{name: name, move: moves[i]}
		}
	}()
	return out
}
```

So if we have 2 of those, we can have another goroutine that is popping "plays" and deciding the winner. At first I just had them return the winner's name, but I liked the reporting Alex's example had so I later added the name and play together so results could be aggregated by the process downstream from the "judge".

```go
type result struct {
	play1, play2 play
	winner       string
}

func makeJudge(player1, player2 <-chan play) <-chan result {
	out := make(chan result)
	go func() {
		for { // ever
			p1 := <-player1
			p2 := <-player2
			out <- result{play1: p1, play2: p2, winner: winnerIs(p1, p2)}
		}
	}()
	return out
}
```

My judge's goroutine uses a `winnerIs` function that returns a string, the winner's name. At first I implemented it like this:

```go
func winnerIs(play1, play2 play) string {
	if play1.move == play2.move {
		return "no one"
	}
	switch play1.move {
	case rock:
		if play2.move == scissors {
			return play1.name
		}
		return play2.name
	case paper:
		if play2.move == rock {
			return play1.name
		}
		return play2.name
	case scissors:
		if play2.move == paper {
			return play1.name
		}
		return play2.name
	}
	return "good job, you broke it!"
}
```

But that felt gross. It didn't read cleanly, and it had an unnecessary return at the end that would never be reached. So I beefed up my test so I knew I had the entire game space mapped:

```go
func TestWinnerIs(t *testing.T) {
	rockPlay := play{name: "rock", move: rock}
	paperPlay := play{name: "paper", move: paper}
	scissorsPlay := play{name: "scissors", move: scissors}

	allMatches := []result{
		{rockPlay, rockPlay, "no one"},
		{rockPlay, paperPlay, "paper"},
		{rockPlay, scissorsPlay, "rock"},
		{paperPlay, rockPlay, "paper"},
		{paperPlay, paperPlay, "no one"},
		{paperPlay, scissorsPlay, "scissors"},
		{scissorsPlay, rockPlay, "rock"},
		{scissorsPlay, paperPlay, "scissors"},
		{scissorsPlay, scissorsPlay, "no one"},
	}

	for _, match := range allMatches {
		winner := winnerIs(match.play1, match.play2)
		if winner != match.winner {
			t.Errorf("%s should have beat %s but got %s", match.play1.move, match.play2.move, winner)
		}
	}
}
```

Now I know I can refactor my `winnerIs` function and ensure it still works the same (I re-read Alex's blog post at this time, too).

```go
var wins = map[move]move{
	rock:     scissors,
	paper:    rock,
	scissors: paper,
}

func winnerIs(play1, play2 play) string {
	if play1.move == play2.move {
		return "no one"
	}
	if wins[play1.move] == play2.move {
		return play1.name
	}
	return play2.name
}
```

This simplified the code and more coherently modeled the game. Each move has a move it ties, it beats, else it loses.

So now if I tie all this together in the `main` function:

```go
player1 := makePlayer("Amon")
player2 := makePlayer("Belinda")
judge := makeJudge(player1, player2)

totals := make(map[string]int)
for i := 0; i < 100000; i++ {
	r := <-judge
	fmt.Printf("%s throws %s\n", r.play1.name, r.play1.move)
	fmt.Printf("%s throws %s\n", r.play2.name, r.play2.move)
	fmt.Printf("%s wins!\n", r.winner)
	totals[r.winner]++
}
fmt.Println(totals)
```

100,000 games takes 550ms, with reporting each match.

```bash
$ go build
$ time ./rps-chans
...
Amon throws scissors
Belinda throws rock
Belinda wins!
Amon throws paper
Belinda throws scissors
Belinda wins!
map[Amon:33192 no one:33219 Belinda:33589]
./rps-chans  0.55s user 0.56s system 118% cpu 0.942 total
```

And with the printing each game removed:

```bash
$ time ./rps-chans
map[Belinda:33400 Amon:33346 no one:33254]
./rps-chans  0.19s user 0.10s system 179% cpu 0.162 total
```

Bump it to a million games:
```
time ./rps-chans
map[Amon:333318 Belinda:333814 no one:332868]
./rps-chans  2.19s user 1.30s system 196% cpu 1.776 total
```

That's what we would expect, right? Using the concurrency primitives in Go makes it easy for our program to leverage multiple cores.

Find the full source on [GitHub][git].

If you want to tinker, check out [this Go playground][play].

[alex]: http://puredanger.github.io/tech.puredanger.com/2013/07/10/rps-core-async/
[git]: https://github.com/danehammer/rps-chans
[play]: https://play.golang.org/p/yj_ny59RaP
