<script>
    // Importation du dispatcher pour créer
    // des custom event
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    // Message a envoyer
    let message = "";
    // Auteur du message
    let author = "";
    // Nombre maximal de caractère d'un message
    let maxLength = 24;
    // Longueur du message en temps réel
    $: nbCaracters = message.length;
    // Désactiver le bouton après un certain nombre de caractères
    $: disabled = message.length > maxLength ? true : false;

    // Ajoute un message à la liste des messages
    const saveMessage = () => {
        // Structure d'un message
        const newMessage = {
            id: Date.now(),
            text: message,
            author: author || 'anonymous',
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
    <!-- Bouton désactiver si disabled est vaut true -->
    <button on:click={saveMessage} disabled={disabled}>Send</button> 
    <!-- Changement de couleurs lors du dépassement du nbre limite de caractère -->
    <span class:alert={nbCaracters > maxLength}>{nbCaracters}</span>
    <!-- Message d'erreur lorsque le bouton est désactivé -->
    {#if disabled}
        <span class="alert"> (message too long)</span>
    {/if}
</main>

<style>
    .text {
        width: 382px;
    }
    .alert {
        color: orangered;
    }
</style>