<script>
    import { onMount } from 'svelte';

    let donations = 2027800; // total donations
    let speed = 200; // speed of counting

    let counterValue = 0;
    
    // start animation/counting
    onMount(() => {
        animate();
    });

    const animate = () => {
        const time = donations / speed;
        if (counterValue < donations) {
            counterValue = Math.ceil(counterValue + time);
            setTimeout(animate, 1);
        } else {
            counterValue = donations;
        }
    }
</script>

<main>
    <div class="donations">
        <h2 class="counter">{counterValue} €</h2>
        <p>Were already donated to Nabu.</p>
    </div>
</main>

<style>
    .counter {
        font-size: 3rem;
        font-weight: bold;
        margin-bottom: 0;
    }

    p {
       font-size: 1.5rem;
    }
</style>