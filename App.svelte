<script>
    import Slider from "./lib/Slider.svelte";
</script>

<main>
    <div class="wrapper">
        <Slider count={9} folder="slider"/>
    </div>
</main>

<style>
    main {
        width: 100%;
    }

    .wrapper {
        max-width: 100%;
        height: 5rem;
        padding: 2rem;
    }
</style>