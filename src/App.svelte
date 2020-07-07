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

    function formatTimer(time) {
        const minutes = new Date(time).getMinutes();
        const seconds = new Date(time).getSeconds();
        let formatted = `${minutes}:`;
        if (seconds === 0) {
            formatted += "00";
        } else if (seconds < 10) {
            formatted += `0${seconds}`;
        } else {
            formatted += `${seconds}`;
        }
        return formatted;
    }
</script>

<svelte:head>
    <link
        href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css"
        rel="stylesheet" />
    <title>Pomodoro Timer</title>
</svelte:head>

<div class='bg-gray-200 h-screen'>

    <header
        class="py-3 text-center text-2xl bg-red-100 shadow-md">
        <h1>Svelte Pomodoro Timer</h1>
    </header>

    <main
        class="flex flex-col justify-center items-center md:w-3/4 mx-auto mt-24 p-8
        bg-red-100 md:rounded shadow-md ">
        <div class="text-6xl font-bold">{formatTimer(currentTime)}</div>

        <div class="space-y-4 flex flex-col">
            {#if !timerOn}
                <button
                    class="px-3 py-1 bg-red-300 border-none rounded
                    hover:bg-red-400 transition-all duration-100 ease-out"
                    on:click={startTimer}
                    type="button">
                    Start Timer
                </button>
            {:else}
                <button
                    class="px-3 py-1 bg-red-300 border-none rounded
                    hover:bg-red-400 transition-all duration-100 ease-out"
                    on:click={pauseTimer}
                    type="button">
                    Pause Timer
                </button>
            {/if}

            <div class="flex space-x-2">
                <button
                    class="px-3 py-1 text-red-800 bg-red-200 rounded
                    hover:bg-red-300 hover:text-red-900 transition-all duration-100 ease-out"
                    on:click={() => setTimer(DEFAULT_DURATION)}
                    type="button">
                    Pomodoro
                </button>
                <button
                    class="px-3 py-1 text-red-800 bg-red-200 rounded
                    hover:bg-red-300 hover:text-red-900 transition-all duration-100 ease-out"
                    on:click={() => setTimer(SHORT_BREAK_DURATION)}
                    type="button">
                    Short Break
                </button>
                <button
                    class="px-3 py-1 text-red-800 bg-red-200 rounded
                    hover:bg-red-300 hover:text-red-900 transition-all duration-100 ease-out"
                    on:click={() => setTimer(LONG_BREAK_DURATION)}
                    type="button">
                    Long Break
                </button>
            </div>
        </div>
    </main>
    <footer class='mx-auto text-center text-sm text-gray-800 p-6 mt-24 md:w-3/4 md:rounded bg-gray-100 shadow'>
        Designed and Developed by Austin Crim
    </footer>
</div>
