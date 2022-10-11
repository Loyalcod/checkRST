<script>
	import page from 'page'
    import Home from './pages/Home.svelte';
    import Result from './pages/Result.svelte';
	

	let current;
	let urlParam

	page('/', ()=> (current = Home))

	page('/result/:email/:regNo', (ctx,next)=>{
		urlParam = ctx.params 
		next()
	},

	()=> (current = Result)
	
	)

	page.start()
</script>

<main>
	<svelte:component this={current} {urlParam}/>
</main>