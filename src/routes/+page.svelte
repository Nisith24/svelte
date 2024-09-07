
<script>
	import { GoogleGenerativeAI } from "@google/generative-ai";

	// Fetch your API_KEY
	const API_KEY = "AIzaSyBCuHXgDG3DHDNfO3Dy1Lpkw0jwizUL3rs";
	const genAI = new GoogleGenerativeAI(API_KEY);
	const model = genAI.getGenerativeModel({ model: "gemini-1.5-flash" });

	let prompt = "";
	let result = "";

	async function getStory() {
		const response = await model.generateContent(prompt);
		result = response.response.text();
    result = result.replace(/\n/g, "<br>");
		console.log(result);

	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<div class="input-group">
		<input
			type="text"
			placeholder="Enter your prompt..."
			bind:value={prompt}
			class="input-field"
		/>
	</div>
	<button class="glossy-button" on:click={getStory}>Generate Story</button>

	<p>{@html result}</p>
</section>

<style>
	.input-group {
		display: flex;
		justify-content: center;
		margin-top: 20px;
	}

	.input-field {
		width: 60%;
		padding: 10px;
		border: 2px solid #ccc;
		border-radius: 10px;
		font-size: 16px;
		outline: none;
		transition: border-color 0.3s ease;
	}

	.input-field:focus {
		border-color: #007bff;
	}

	.glossy-button {
		display: block;
		width: 200px;
		margin: 20px auto;
		padding: 15px;
		background: linear-gradient(145deg, #007bff, #00cfff);
		border: none;
		border-radius: 25px;
		color: white;
		font-size: 16px;
		font-weight: bold;
		cursor: pointer;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		transition: transform 0.2s, box-shadow 0.2s;
	}

	.glossy-button:hover {
		transform: scale(1.05);
		box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
	}
</style>