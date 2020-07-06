<script>
    const DEFAULT_DURATION = 60000 * 25;
    const LONG_BREAK_DURATION = 60000 * 10;
    const SHORT_BREAK_DURATION = 60000 * 5;
    let currentTime = DEFAULT_DURATION;
    let timerInterval;
    let timerOn = false;

    function setTimer(seconds) {
        currentTime = seconds;
    }

    function pauseTimer() {
        timerOn = false;
        clearInterval(timerInterval);
    }

    function startTimer() {
        timerOn = true;
        timerInterval = setInterval(() => (currentTime -= 1000), 1000);
    }
</script>

<svelte:head>
    <link
        href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css"
        rel="stylesheet" />
</svelte:head>

<header class='py-3 text-center text-2xl bg-red-100 border-b-2 border-red-200'>
	<h1>Svelte Pomodoro Timer</h1>
</header>

<main class="flex flex-col justify-center items-center p-8 bg-red-100">
    <div class="text-6xl font-bold">
        {new Date(currentTime).getMinutes()}:{new Date(currentTime).getSeconds() === 0 ? new Date(currentTime).getSeconds() + '0' : new Date(currentTime).getSeconds()}
    </div>

    <div class="space-y-4 flex flex-col">
        {#if !timerOn}
            <button
                class="px-3 py-1 bg-red-300 border-none rounded hover:bg-red-400
                transition-all duration-100 ease-out"
                on:click={startTimer}
                type="button">
                Start Timer
            </button>
        {:else}
            <button
                class="px-3 py-1 bg-red-300 border-none rounded hover:bg-red-400
                transition-all duration-100 ease-out"
                on:click={pauseTimer}
                type="button">
                Pause Timer
            </button>
        {/if}

        <div class='flex space-x-2'>
            <button
                class="px-3 py-1 bg-red-300 border-none rounded hover:bg-red-400
                transition-all duration-100 ease-out"
                on:click={() => setTimer(DEFAULT_DURATION)}
                type="button">
                Pomodoro
            </button>
            <button
                class="px-3 py-1 bg-red-300 border-none rounded hover:bg-red-400
                transition-all duration-100 ease-out"
                on:click={() => setTimer(SHORT_BREAK_DURATION)}
                type="button">
                Short Break
            </button>
            <button
                class="px-3 py-1 bg-red-300 border-none rounded hover:bg-red-400
                transition-all duration-100 ease-out"
                on:click={() => setTimer(LONG_BREAK_DURATION)}
                type="button">
                Long Break
            </button>
        </div>
    </div>
</main>
