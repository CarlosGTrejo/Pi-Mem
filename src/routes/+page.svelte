<script>
    const pi =
        "3.141592653589793238462643383279502884197169399375105820974944592307816406286208998628034825342117067982148086513282306647093844609550582231725359408128";
    let idx = 2;
    let digits = "3.";
    let guess = " ";
    let correct = false;
    let strikes = 0;
    let score = 1;

    function onKeyDown(e) {
        console.dir(e)
        // check if key pressed is numeric (space bar ' ' is perceived as zero by isNaN)
        if (e.code != 'Space' && !isNaN(e.key)) {  // Check number
            guess = e.key;
            check();
        } else if (e.code == 'Space') {  // Reset Game
            idx = 2;
            digits = '3.';
            guess = ' ';
            correct = 'false';
            strikes = 0;
            score = 1;
        }
    }

    function check() {
        if (guess == pi[idx]) { // correct guess
            digits += guess;
            idx++;
            score++;
            correct = true;
        } else {  // incorrect
            correct = false;
            strikes++;
        }
        if (strikes >= 3) {
            digits = pi;
        }
    }
</script>

<div class="content">
    <h1 class='title'>Pi Mem</h1>
    <p class='score'>Score: {score}</p>
    <p class='pi'>{digits}</p>
    <p class='guess incorrect' class:correct>{guess}</p>
    <div class='strikes'>
        <div class="box {(strikes >= 1) ? 'cross' : ''}"/>
        <div class="box {(strikes >= 2) ? 'cross' : ''}"/>
        <div class="box {(strikes >= 3) ? 'cross' : ''}"/>
    </div>
</div>

<svelte:window on:keydown={onKeyDown} />

<style>
    /* @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Mono:wght@700&display=swap'); */
    @import url('https://fonts.googleapis.com/css2?family=Chivo+Mono:wght@700&display=swap');
    .content {
        display: grid;
        background-color: #F0EBD8;
        height: 100vh;
        overflow: hidden;
        grid-template:
            [header-start]  "title . score" auto [header-end]
            [pi-start]      "pi pi pi" 1fr [pi-end]
            [guess-start]   " . guess ." auto [guess-end]
            [strikes-start] " . strikes . " auto [strikes-end]
            / 1fr 1fr 1fr;
        font-family: 'Chivo Mono', sans-serif;
        font-weight: bold;
        font-size: 48px;
        padding: 0.6em 1em;
    }
    .title {
        font-size: 48px;
        grid-area: title;
        justify-self: start;
        align-self: center;
        margin: 0;
    }
    .score {
        grid-area: score;
        justify-self: end;
        align-self: center;
    }
    .strikes {
        grid-area: strikes;
        display: flex;
        justify-content: space-around;
        padding: 0 1em;
    }
    .guess {
        grid-area: guess;
        min-height: 1.4em;
        font-size: 1.4em;
        place-self: end center;
    }
    .pi {
        font-size: 1.4em;
        grid-area: pi;
        white-space: normal;
        word-wrap: break-word;
        word-break: break-all;
        margin: 0.5em 0px;
        overflow-y: auto;
    }

    .incorrect {
        color: #BC4749;
    }
    .correct {
        color: #6A994E;
    }

    .box {
        height: 1.4em;
        width: 1.4em;
        outline: solid 5px black;
        border-radius: 5px;
    }

    .cross::after {
        position: absolute;
        margin: 0;
        content: "\274c";
        font-size: 1em;
        color:#BC4749;
        line-height: 1.4em;
        text-align: center;
    }
</style>
