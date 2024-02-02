<script lang="ts">
	export let label: string = '';
	export let style: string = '';
	export let onClick: () => void;
</script>

<button
	type="submit"
	on:click={onClick}
	class={`cursor-pointer px-3 py-1 text-base text-white ${style}`}
>
	{label}
</button>
