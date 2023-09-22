<script>
    const pi =
        "3.141592653589793238462643383279502884197169399375105820974944592307816406286208998628034825342117067982148086513282306647093844609550582231725359408128";
    let idx = 2;
    let digits = "3.";
    let guess = "";
    let correct = false;
    let strikes = 0;

    function onKeyDown(e) {
        guess = e.key;
        check();
    }

    function check() {
        if (strikes == 3) {
            digits = pi;
        } else if (guess == pi[idx]) {
            digits += guess;
            idx++;
            correct = true;
        } else {
            correct = false;
            strikes++;
        }
    }
</script>

<div class="content">
    <b class="incorrect">Strike {strikes}</b>
    <b class="incorrect" class:correct>{guess}</b>
    <p>{digits}</p>
</div>

<svelte:window on:keydown={onKeyDown} />

<style>
    .content {
        display: grid;
        grid-template:
            [strikes-start] "strikes" 1fr [strikes-end]
            [guess-start] "guess" 2fr [guess-end]
            [output-start] "output" 2fr [output-end]
            / auto;
        place-items: center;
    }

    .incorrect {
        color: red;
    }

    .correct {
        color: green;
    }
</style>
