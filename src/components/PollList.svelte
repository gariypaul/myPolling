<script>
    import PollDetails from "./PollDetails.svelte";
    import PollStore from "../stores/PollsStore.js";
    import { onDestroy, onMount } from "svelte";
   
</script>

<div class="poll-list">
    <!--Use $Pollstore to actively subscribe and unscribe to pollstore data-->
    {#each $PollStore as poll (poll.id)}
      <PollDetails {poll} on:vote/>
    {/each}
</div>

<style>
    .poll-list{
        display:grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>