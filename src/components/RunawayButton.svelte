<script>
    import { onMount } from "svelte";
    import anime from "animejs";

    let button; // This is used to reference the button in the DOM

    // Function to animate the movement of the button
    const animateMove = (element, prop, pixels) =>
        anime({
            targets: element,
            [prop]: `${pixels}px`,
            easing: "easeOutCirc",
        });

    // Function to get a random number within the range of 0 to num
    const getRandomNumber = (num) => Math.floor(Math.random() * (num + 1));

    onMount(() => {
        // Adding event listeners for mouseover and click events
        ["mouseover", "click"].forEach((eventType) => {
            button.addEventListener(eventType, (event) => {
                const top = getRandomNumber(
                    window.innerHeight - button.offsetHeight,
                );
                const left = getRandomNumber(
                    window.innerWidth - button.offsetWidth,
                );

                animateMove(button, "left", left).play();
                animateMove(button, "top", top).play();
            });
        });
    });
</script>

<button bind:this={button} id="runaway-btn">No</button>

<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
        user-select: none;
    }

    body {
        background-color: rgb(31, 31, 31);
    }

    button {
        position: absolute;
        height: 4rem;
        width: 10rem;
        font-size: 1.5rem;
        border-radius: 5px;
        border: none;
        box-shadow: 1px 1px 5px black;
        background-color: white;
        margin-left: 5px;
        left: 50%;
    }

    button:hover {
        box-shadow: 0 0 0 4px rgba(255, 105, 180, 0.5); /* Pink ring */
        cursor: pointer; /* Changes the cursor to a pointer to indicate it's clickable */
    }
</style>
