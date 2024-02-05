<script>
	import { goto } from "$app/navigation";
	import Counter from "./Counter.svelte";
	import RunawayButton from "../components/RunawayButton.svelte";
	let heart; // Reference to the heart element
	let clickCount = 0; // Initialize the click counter
	const requiredClicks = 10; // Number of clicks required to activate

	function handleClick() {
		clickCount++; // Increment the click counter
		console.log(`Button clicked ${clickCount} times`);

		if (clickCount >= requiredClicks) {
			console.log("Activating the heart and navigating");
			heart.classList.add("heart-animate");

			heart.style.opacity = "1";
			heart.style.transform = "translate(-50%, -50%) scale(30)";
			// clickCount = 0;

			setTimeout(() => {
				goto("/yes");
			}, 1000); // Adjusted for demonstration, set according to your animation
		}
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<div class="container">
		<h1>Will you be my Valentine?</h1>
		<h4>try saying no if you dare...</h4>
		<p>You need {requiredClicks - clickCount} more yeses.</p>
		<img src="../bear.png" alt="" />
		<div class="heart" bind:this={heart}>❤️</div>
		<div class="button-container">
			<button on:click={handleClick}>Yes</button>
			<RunawayButton />
		</div>
	</div>
</section>

<style>
	h1,
	h4 {
		margin: auto;
		padding: auto;
	}

	section {
		/* display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center; */
	}

	.container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.button-container {
		display: flex;
		flex-direction: row;
		flex-grow: 1;
		left: 50%;
		padding: 20px;
	}

	button {
		height: 4rem;
		width: 10rem;
		font-size: 1.5rem;
		border-radius: 5px;
		border: none;
		box-shadow: 1px 1px 5px black;
		background-color: white;
		transform: translateX(-50%);
		margin-right: 5px;
	}

	button:hover {
		box-shadow: 0 0 0 4px rgba(255, 105, 180, 0.5); /* Pink ring */
		cursor: pointer; /* Changes the cursor to a pointer to indicate it's clickable */
	}

	.heart {
		/* Remove the duplicate font-size declaration */
		font-size: 5rem; /* Initial font size */
		position: fixed;
		top: 50%;
		left: 50%;
		z-index: 1000;
		/* Start with a small scale */
		transform: translate(-50%, -50%) scale(0.1); /* Adjust the initial scale as needed */
		transition: transform 2s ease; /* Adjusted for a smoother transition */
		color: red; /* Ensure the heart is a visible color */
		opacity: 0; /* Start invisible if you prefer */
	}

	.heart-animate {
		transform: translate(-50%, -50%) scale(10); /* Scale up */
		opacity: 1; /* Ensure full visibility when animating */
	}
</style>
