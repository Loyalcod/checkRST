<script>
    import { fade } from "svelte/transition";


fade
export let showInModel;

</script>

{#if showInModel}
<!-- svelte-ignore a11y-click-events-have-key-events -->
<div in:fade out:fade on:click|self class="model">
    <div class="mainModel">
        <slot></slot>
    </div>
</div>
{/if}

<style>
    .model{
        width: 100vw;
        height: 100vh;
        position: fixed;
        background: rgba(0, 0, 0, 0.8)
    }

    .mainModel{
        max-width: 400px;
        margin: 10% auto;
        background: white;
        border-radius: 10px;
        padding: 10px;
    }
</style>