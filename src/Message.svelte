<script>
    // Importation du dispatcher pour créer
    // des custom event
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    // Message a envoyer
    let message = "";
    // Props author
    export let author;
    // Ajoute un message à la liste des messages
    const saveMessage = () => {
        // Structure d'un message
        const newMessage = {
            id: Date.now(),
            text: message,
            author: author,
        };
        // Ajout du message au début de la liste des messages
        //messages = [newMessage, ...messages];
        console.log('newMessage', newMessage);
        // Dispatcher l'event message et passer le payload newMessage
        dispatch('message', newMessage);
        // Reset de la variable message
        message = "";
    }
</script>

<main>
    <textarea cols="50" rows="5" bind:value={message}></textarea>
    <br>
    <button on:click={saveMessage}>Send</button>
</main>

<style></style>