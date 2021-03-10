<script>
	export let name;
    let message = "";
    let messages = [];

    const updateMessage = (event) => {
        console.log(event.target.value);
        message = event.target.value;
    }
    
    const saveMessage = () => {
        const newMessage = {
            id: Date.now(),
            text: message,
            author: "Jonathan"
        };

        messages = [newMessage, ...messages];
        console.log('messages', messages);
    }
</script>

<main>
	<h1>{name}!</h1>
    <textarea cols="50" rows="5" on:input={updateMessage}></textarea>
    <br>
    <button on:click={saveMessage}>Send</button>
    <div>
        <h3>Preview</h3>
        {message}
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