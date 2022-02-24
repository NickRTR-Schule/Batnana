<script>
    import { onMount } from 'svelte';

    const bananaPrice = 0.5;
    const boughtBananas = 823479;
    const values = {
        boughtBananas,
        donatedEuros: boughtBananas * (bananaPrice * 0.2)
    }
    const duration = 1000; // duration of counting
    const minspeed = 10; // minimal animation speed

    let counter = {
        boughtBananas: 0,
        donatedEuros: 0
    };

    // round number and place dots every three digits
    function formatNumber(x) {
        x = Number(Math.round(x + 'e2') + 'e-2');
        var parts = x.toString().split(".");
        parts[0]=parts[0].replace(/\B(?=(\d{3})+(?!\d))/g,".");
        return parts.join(",");
    }
    
    // start animation/counting
    onMount(() => {
        let timers = [];
        for (let [key, value] of Object.entries(values)) {
            let step = 1;
            while((duration / (value / step)) < minspeed){
                step++;
            }
            timers[key] = setInterval(function(){
                if(counter[key] < value){
                    counter[key] += step;
                } else {
                    counter[key] = value;
                    clearInterval(timers[key]);
                }
            }, duration / (value / step));
        }
    });
</script>

<main>
    <div class="donatedEuros">
        <p>Sold Bananans:</p>
        <h2 class="counter">{counter.boughtBananas}</h2>
        <p>Therefore donated:</p>
        <h2 class="counter">{formatNumber(counter.donatedEuros)} €</h2>
    </div>
</main>

<style>
    .counter {
        font-size: 3rem;
        font-weight: bold;
        margin: 0;
    }

    p {
       font-size: 1.5rem;
    }
</style>