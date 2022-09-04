<script>
    import {onDestroy, onMount} from 'svelte'

    export let count = 0
    export let folder = ""

    $: hasFolder = folder !== "" ? "/" : ""

    let slider
    let scrollEnabled = true

    function scroll() {
        let rows = document.getElementsByClassName('row')


        slider.scrollLeft += 1

        if (scrollEnabled && rows[1].getBoundingClientRect().left <= slider.getBoundingClientRect().left) {
            slider.scrollLeft = 0
        }
        scrollEnabled = rows[0].clientWidth > slider.clientWidth;
    }

    onMount(() => {
        slider = document.getElementsByClassName('slider')[0]

        slider.addEventListener('scroll', scroll)
        window.addEventListener('load', scroll)
        window.addEventListener('resize', scroll)
    })

    onDestroy(() => {
        slider.removeEventListener('scroll', scroll)
        window.removeEventListener('load', scroll)
        window.removeEventListener('resize', scroll)
    })
</script>

<div class="slider" style={!scrollEnabled ? 'justify-content: center': ''}>
    <div class="row">
        {#each Array(count) as _, id}
            <img src="../src/assets/{folder}{hasFolder}{id}.jpg" class="logo" alt="{id}">
        {/each}
    </div>

    {#if scrollEnabled}
        <div class="row">
            {#each Array(count) as _, id}
                <img src="../src/assets/{folder}{hasFolder}{id}.jpg" class="logo" alt="{id}">
            {/each}
        </div>
    {/if}
</div>

<style>
    .slider {
        width: 100%;
        height: 100%;
        white-space: nowrap;
        overflow-x: hidden;

        display: flex;
        flex-flow: row nowrap;
        align-items: center;
        justify-content: flex-start;
    }

    .row {
        display: flex;
        flex-flow: row nowrap;
        align-items: center;
        justify-content: flex-start;
        height: 100%;
    }

    .logo {
        display: inline-flex;
        margin: 0 2rem;
        height: 100%;
    }
</style>