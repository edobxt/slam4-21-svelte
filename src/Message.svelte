<script>
    // Importation du dispatcher pour créer
    // des custom event
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    // Message a envoyer
    let message = "";
    // Auteur du message
    let author = "";
    // Longueur du message en temps réel
    $: nbCaracters = message.length;

    // Ajoute un message à la liste des messages
    const saveMessage = () => {
        // Structure d'un message
        const newMessage = {
            id: Date.now(),
            text: message,
            author: author,
            date: new Date(),
        };
        // Ajout du message au début de la liste des messages
        //messages = [newMessage, ...messages];
        console.log('newMessage', newMessage);
        // Dispatcher l'event message et passer le payload newMessage
        dispatch('message', newMessage);
        // Reset de la variable message
        message = "";
        // Reset de la variable author
        author = "";
    }
</script>

<main>
    <input class="text" type="text" bind:value={author}>
    <br>
    <textarea cols="50" rows="5" bind:value={message}></textarea>
    <br>
    <button on:click={saveMessage}>Send</button><span>{nbCaracters}</span>
</main>

<style>
    .text {
        width: 382px;
    }
</style>