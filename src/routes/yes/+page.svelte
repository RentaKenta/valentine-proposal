<script>
    import { onMount } from "svelte";

    let heart; // Reference to the heart element

    onMount(() => {
        // Force a reflow to ensure initial styles are applied
        const _ = heart.offsetHeight; // Accessing offsetHeight forces a reflow

        // Set up the animation immediately after forcing reflow
        heart.style.opacity = "0";
        heart.style.transform = "translate(-50%, -50%) scale(0)";
        heart.style.transition = "transform 1s ease, opacity 1s ease";

        heart.addEventListener("transitionend", () => {
            console.log("Heart animation finished");
            // Actions to take after the animation ends
            heart.style.display = "none";
        });
    });
</script>

<div class="main">
    <div class="heart" bind:this={heart}>❤️</div>

    <h1>Congrats!!! You're My Valentine Now C:</h1>
    <img src="/milk-and-mocha.gif" alt="" />
</div>

<style>
    .heart {
        font-size: 5rem;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) scale(25); /* Initially large */
        color: red;
        opacity: 1; /* Initially fully visible */
        z-index: 1000;
    }

    .main {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .main img {
        scale: 200%;
        margin-top: 10%;
    }
</style>
