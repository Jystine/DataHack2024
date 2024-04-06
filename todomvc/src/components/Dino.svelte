<script>
    let imageFile;
    let result = '';

    async function classifyImage() {
        if (!imageFile) {
            alert('Please select an image.');
            return;
        }

        const formData = new FormData();
        formData.append('file', imageFile);

        try {
            const response = await fetch('/classify', {
                method: 'POST',
                body: formData
            });
            const data = await response.json();
            result = data.predictions.join(', ');
        } catch (error) {
            console.error('Error:', error);
        }
    }
</script>

<div class="container">
    <h1>Image Classification</h1>
    <input type="file" accept="image/*" on:change={e => imageFile = e.target.files[0]}>

    <button on:click={classifyImage}>Classify</button>

    {#if result}
        <div id="result">
            <h2>Classification Result:</h2>
            <p>{result}</p>
        </div>
    {/if}
</div>

<style>
    .container {
        max-width: 600px;
        margin: 0 auto;
        text-align: center;
    }

    h1 {
        margin-bottom: 20px;
    }

    input[type="file"] {
        margin-bottom: 20px;
    }

    button {
        padding: 10px 20px;
        background-color: #007bff;
        color: #fff;
        border: none;
        cursor: pointer;
    }

    #result {
        margin-top: 20px;
    }
</style>