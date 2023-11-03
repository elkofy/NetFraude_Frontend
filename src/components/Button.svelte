<script>
	
	let buttonProps = {
	class:[$$restProps.class]
	}

    export let onclick 
</script>
	<button on:click = {onclick}>

			<slot/>
	</button>

<style>
	.primary{
		color:green;
	}
	.danger {
		color:red;
	}
	.sm {
		font-size:1em;
		padding:0.1em;
	}
	.lg {
		font-size:2em
	}
</style>