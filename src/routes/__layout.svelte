<body>
    <nav>
        <h1 on:click={() => {location.reload()}}>Batnana</h1>
        <img src="/favicon.svg" alt="" on:click={() => {location.reload()}}>
    </nav>
    <slot></slot>
    <footer>
        <hr>
        <p style="margin: .5rem;">All Numbers are examples, Batnana school project.</p>
    </footer>
</body>

<style>
    * {
		margin: 0;
		font-family: Arial, Helvetica, sans-serif;
        text-align: center;
	}

    body {
        background-color: var(--accent);
    }

	nav {
        background-color: black;
        color: var(--accent);
        font-size: 1.5rem;
		display: flex;
		justify-content: space-between;
		align-items: center;
        padding: .5rem;
	}

    h1 {
        cursor: pointer;
    }

	img {
		width: 4rem;
        cursor: pointer;
	}

    /* Variables */
    :global(:root) {
        --accent: #F8B323;
    }

    /* global styles */
    :global(a) {
        text-decoration: underline;
        color: black;
    }

    :global(hr) {
        border: 1px solid black;
    }
</style>