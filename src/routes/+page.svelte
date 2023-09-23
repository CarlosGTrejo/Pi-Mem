<script>
    const pi =
        "3.141592653589793238462643383279502884197169399375105820974944592307816406286208998628034825342117067982148086513282306647093844609550582231725359408128";
    let idx = 2;
    let digits = "3.";
    let guess = "";
    let correct = false;
    let strikes = 0;
    let score = 1;

    function onKeyDown(e) {
        console.dir(e)
        // check if key pressed is numeric (space bar ' ' is perceived as zero by isNaN)
        if (e.code != 'Space' && !isNaN(e.key)) {
            guess = e.key;
            check();
        }
    }

    function check() {
        if (strikes == 3) {
            digits = pi;
        } else if (guess == pi[idx]) { // correct guess
            digits += guess;
            idx++;
            score++;
            correct = true;
        } else {  // incorrect
            correct = false;
            strikes++;
        }
    }
</script>

<div class="content">
    <h1 class='title'>Pi Mem</h1>
    <p class='score'>Score: {score}</p>
    <p class='pi'>{digits}</p>
    <p class='guess incorrect' class:correct>{guess}</p>
    <p class='strikes'>Strike {strikes}</p>
</div>

<svelte:window on:keydown={onKeyDown} />

<style>
    .content {
        display: grid;
        background-color: #F0EBD8;
        height: 100vh;
        grid-template:
            [header-start]  "title . score" 1fr [header-end]
            [pi-start]      "pi pi pi" 3fr [pi-end]
            [guess-start]   " . guess ." 1fr [guess-end]
            [strikes-start] " . strikes . " 1fr [strikes-end]
            / 1fr 1fr 1fr;
        font-family: sans-serif;
        font-weight: bold;
        font-size: 48px;
        padding: 0.6em 1em;
    }
    .title {
        font-size: 48px;
        grid-area: title;
        justify-self: start;
        align-self: center;
    }
    .score {
        grid-area: score;
        justify-self: end;
        align-self: center;
    }
    .strikes {
        grid-area: strikes;
        place-self: center;
    }
    .guess {
        grid-area: guess;
        min-height: 1em;
        place-self: center;
    }
    .pi {
        grid-area: pi;
        white-space: normal;
    }

    .incorrect {
        color: #BC4749;
    }
    .correct {
        color: #6A994E;
    }
</style>
