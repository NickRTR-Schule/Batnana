<body>
    <nav>
        <h1>Batnana</h1>
        <img src="/favicon.svg" alt="">
    </nav>
    <slot></slot>
</body>

<style>
    * {
		margin: 0;
		font-family: Arial, Helvetica, sans-serif;
        text-align: center;
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

	img {
		width: 4rem;
	}

    /* Variables */
    :global(:root) {
        --accent: #F8B323;
    }
</style>