<script>
    import { text } from "svelte/internal";
    import Message from "./Message.svelte";

    // Nom de l'application
	export let name;
    // Liste des messages
    let messages = [];
    // Variable flag
    let isVisible = true;

    // Fonction permettant d'ajouter un message
    // en utilisant le custom event message
    const addMessage = (event) => {
        // Récupération du message
        // dans le custom event
        console.log(event.detail);
        // Ajout du message
        // dans la liste des messages
        messages = [event.detail, ...messages];
    }

    // Options du format de la date d'ajout d'un message
    const options = {
        weekday: "long",
        year: "numeric",
        month: "long",
        day: "numeric",
        hour12: true,
        hour: "numeric",
        minute: "2-digit",
        second: "2-digit",
    };

    // Formatter de la date
    const formatter = new Intl.DateTimeFormat("en-US", options);

    // Toggle sur la visibilité du component Message
    const toggle = () => {
        isVisible = !isVisible;
    }
</script>

<main>
	<h1>{name}!</h1>

    <div>
        <button on:click={toggle}>{isVisible ? 'hide' : 'show'}</button>
        <br>
    </div>

    {#if isVisible}
    <Message on:message={addMessage}/>
    {/if}

    <div>
        <h2>Messages</h2>
        <!-- Parcourir la liste des messages -->
        {#each messages as message}
            <!-- Auteur du message -->
            <div class="author">By {message.author} on {formatter.format(message.date)}</div>
            <!-- Contenu du message -->
            <div>{message.text}</div>
            <!-- Barre de séparation -->
            <hr>
        {/each}
    </div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

    .author {
        font-weight: bold;
    }
</style>