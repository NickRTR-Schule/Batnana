<script>
    import { onMount } from 'svelte';

    const bananaPrice = 0.5;
    const boughtBananas = new Date().getTime();
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
    <article>
        <h3 class="slogan">We will save the bats, while you're eating our tasty banana.</h3>
        <p class="info">For every bought Batnana, we are going to donate 10 cents to the <a href="https://www.nabu.de/" target="_blank">Nabu</a> organisation, to ensure the protection of the variety of animal species.</p>
        <a href="https://www.nabu.de/" target="_blank"><img src="/Nabu-logo.png" alt="Nabu icon"></a>
    </article>
    <hr>
    <div class="stats">
        <p>Sold Bananas:</p>
        <h2 class="counterValue">{counter.boughtBananas}</h2>
        <p>Therefore donated money:</p>
        <h2 class="counterValue">{formatNumber(counter.donatedEuros)} €</h2>
    </div>

    <div class="video">
        <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/S8zhnXZdTFM" title="Bat eating a banana" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</main>

<style>
    main {
        padding-top: 1rem;
        margin: 0 .5rem;
    }

    article h3 {
        margin: 0;
    }

    article p {
        font-size: 1.1rem;
        margin: .5rem 0;
    }

    article img {
        height: 4rem;
        background-color: white;
        padding: .5rem;
        border-radius: 1rem;
    }

    hr {
        border: 1px solid black;
    }

    .counterValue {
        font-size: 3rem;
        font-weight: bold;
        margin: 0;
    }

    .stats p {
        margin: 0;
        font-size: 1.5rem;
    }

    .video {
        margin-top: 1rem;
    }

    iframe {
        /* width / 1.778 = height */
        width: 95vw; 
        max-width: 750px;
        max-height: 421.8px;
        height: 53.5vw; /* 100/56.25 = 560/315 = 1.778 */  
        border-radius: .5rem;
    }
</style>