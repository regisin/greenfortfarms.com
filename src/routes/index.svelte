<script>
    import { onMount } from 'svelte';
    import { browser } from '$app/env';

    let remaining = {
        weeks: 0,
        days: 0,
        hours: 0,
        minutes: 0,
        seconds: 0,
        done: true
    }
    let timer;

    const countDownDate = new Date("May 22, 2022 12:00:00").getTime();
    const now = new Date().getTime();
    let timeleft = countDownDate - now;
    
    onMount(async () => {
        if (browser) {
            timer = setInterval(function() {
                if(timeleft > 0){
                    remaining.weeks = Math.floor(timeleft / (1000 * 60 * 60 * 24 * 7));
                    remaining.days = Math.floor((timeleft % (1000 * 60 * 60 * 24 * 7)) / (1000 * 60 * 60 * 24));
                    remaining.hours = Math.floor(((timeleft % (1000 * 60 * 60 * 24 * 7)) % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                    remaining.minutes = Math.floor((((timeleft % (1000 * 60 * 60 * 24 * 7)) % (1000 * 60 * 60 * 24)) % (1000 * 60 * 60)) / (1000 * 60));
                    remaining.seconds = Math.floor(((((timeleft % (1000 * 60 * 60 * 24 * 7)) % (1000 * 60 * 60 * 24)) % (1000 * 60 * 60)) % (1000 * 60)) / 1000);
                    // remaining.seconds = Math.floor((timeleft % (1000 * 60)) / 1000);
                    remaining.done = false;
                    timeleft-=1000;
                } else {
                    remaining.days = 0;
                    remaining.hours = 0;
                    remaining.minutes = 0;
                    remaining.seconds = 0;
                    remaining.done = true;
                    clearInterval(timer);
                }

            }, 1000)
        }
    })

</script>

<h1>
    {#if remaining.done === false}
    {remaining.weeks} weeks 
    {remaining.days} days 
    {remaining.hours} hours 
    {remaining.minutes} minutes 
    {remaining.seconds} seconds 
    {:else}
    <h2>The time has come!</h2>
    {/if}
</h1>