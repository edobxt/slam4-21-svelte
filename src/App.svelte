<script>
    import { text } from "svelte/internal";
    import Message from "./Message.svelte";
    // Nom de l'application
	export let name;
    // Liste des messages
    let messages = [];
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
</script>

<main>
	<h1>{name}!</h1>
    
    <Message author="Jojo" on:message={addMessage}/>

    <div>
        <h2>Messages</h2>
        <!-- Parcourir la liste des messages -->
        {#each messages as message}
            <!-- Auteur du message -->
            <div class="author">By {message.author}</div>
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