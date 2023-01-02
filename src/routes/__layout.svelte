<body>
    <nav>
        <h1 on:click={() => {location.reload()}}>Batnana</h1>
        <img src="/favicon.svg" alt="" on:click={() => {location.reload()}}>
    </nav>
    <main><slot></slot></main>
    <footer>
        <p>©2023 Nick Reutlinger, Batnana is a school project.</p>
    </footer>
</body> 

<style>
    * {
		margin: 0;
        font-family: 'Segoe UI', Tahoma, Verdana, sans-serif;
        text-align: center;
	}   

    body {
        background-color: var(--accent);
        background-image: url(/banana.jpg);
        background-size: contain;
        background-position: center;
    }
    
    main {
        margin: 0 auto;
        max-width: 900px;
    }

    main {
        padding: 0 1rem;
    }

    footer {
        background-color: var(--card);
        padding: .5rem;
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
        --card: beige;
    }

    /* global styles */
    :global(a) {
        text-decoration: underline;
        color: black;
    }

    :global(.card) {
        background-color: var(--card);
        border: 4px solid black;
        border-radius: 2rem;
        padding: 1rem;
        margin-bottom: 1rem !important;
    }
</style>
