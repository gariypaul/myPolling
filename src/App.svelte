<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';

	let items = ["Current Polls", "Add New Poll"];
	let activeItem = "Current Polls";

</script>


<Header/>
<main>
	<h1>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Consequat interdum varius sit amet mattis vulputate enim nulla aliquet</h1>
</main>
<Footer/>




<style>
	main{
		max-width:960px;
		margin: 40px auto;
	}
</style>

