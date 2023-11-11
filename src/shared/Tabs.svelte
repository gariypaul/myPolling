<script>
    import { createEventDispatcher } from "svelte";
    const dipatch = createEventDispatcher();
    export let items;
    export let activeItem;
</script>

<div class="tabs">
    <ul>
        {#each items as item}
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <li on:click={()=>dipatch('tabChange', item)}>
                <div class:active={item===activeItem}>{item}</div>
            </li>
        {/each}
    </ul>
</div>

<style>
    .tabs{
        margin-bottom: 40px;
    }
    ul{
        display: flex;
        justify-content: center;
        padding: 0px;
        list-style-type: none;
    }
    li{
        margin: 0 16px;
        font-size: 18px;
        color: #555;
        cursor: pointer;
    }
    .active{
        color: #d91b42;
        border-bottom:2px solid #d91b42 ;
        padding-bottom: 8px;
    }
</style>