<script>
    import { onMount } from 'svelte';

    const bananaPrice = 0.5;
    const boughtBananas = 102043;
    const values = {
        boughtBananas,
        donatedEuros: boughtBananas * (bananaPrice * 0.2)
    }
    const duration = 1500; // duration of counting
    const minspeed = 10; // minimal counting speed

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
    <article class="card">
        <h1 class="slogan">We will save the bats, while you're eating our tasty banana.</h1>
        <p class="info">For every bought Batnana, we are going to donate 10 cents to the <a href="https://www.nabu.de/" target="_blank">Nabu</a> organisation, in order to ensure the protection of the variety of animal species.</p>
        <a href="https://www.nabu.de/" target="_blank"><img src="/Nabu-logo.png" alt="Nabu icon"></a>
    </article>
    <div class="stats card">
        <p>Sold Bananas:</p>
        <h2 class="counterValue">{formatNumber(counter.boughtBananas)}</h2>
        <p>Therefore donated money:</p>
        <h2 class="counterValue">{formatNumber(counter.donatedEuros)} €</h2>
    </div>
    <div class="motivation card">
        <h2>Our Motivation:</h2>
        <iframe src="https://www.youtube-nocookie.com/embed/S8zhnXZdTFM" title="Bat eating a banana" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</main>

<style>
    main {
        padding-top: 1rem;
    }

    article h1 {
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

    .counterValue {
        font-size: 3rem;
        font-weight: bold;
        margin: 0;
    }

    .stats p {
        margin: 0;
        font-size: 1.5rem;
    }

    .motivation h2 {
        margin: 0;
        margin-bottom: .9rem;
    }

    iframe {
        /* width / 1.778 = height */
        width: 80vw; 
        max-width: 800px;
        max-height: 449.94px;
        height: 45vw; /* 100/56.25 = 560/315 = 1.778 */  
        border-radius: .5rem;
    }

    @media only screen and (max-width: 600px) {
        .stats h2 {
            font-size: 2.2rem;
        }
    }
</style>