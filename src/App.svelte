<script>
    import { text } from "svelte/internal";
    import Message from "./Message.svelte";
    // Nom de l'application
	export let name;
    // Liste des messages
    let messages = [];
</script>

<main>
	<h1>{name}!</h1>
    
    <Message author="Jojo"/>

    <div>
        <h2>Messages</h2>
        <!-- Parcourir la liste des messages -->
        {#each messages as message}
            <!-- Auteur du message -->
            <div>By {message.author}</div>
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
</style>