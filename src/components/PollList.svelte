<script>
    import PollDetails from "./PollDetails.svelte";
    import PollStore from "../stores/PollsStore.js";
   
</script>

<div class="poll-list">
    <!--Use $Pollstore to actively subscribe and unscribe to pollstore data-->
    {#each $PollStore as poll (poll.id)}
      <PollDetails {poll}/>
    {/each}
</div>

<style>
    .poll-list{
        display:grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>