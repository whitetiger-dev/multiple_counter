<script lang="ts">
	import Button from './Button.svelte';

	export let key: number = 0;
	export let counter: { title: string; value: number };
	export let onIncrease: (key: number) => void;
	export let onDecrease: (key: number) => void;
	export let onInitialize: (key: number) => void;
	export let onRemove: (index: number) => void;
</script>

<div
	class="max-w-sm rounded border-solid bg-gray-100 shadow-lg gap-8 flex relative items-center px-4 py-1"
>
	<input bind:value={counter.title} class="px-2 text-gray-500 w-32" />
	<span class="font-bold">{counter.value}</span>
	<div class="flex flex-row">
		<Button
			style="rounded-tl-md rounded-bl-md bg-red-400"
			label="+"
			onClick={() => onIncrease(key)}
		/>
		<Button style="bg-blue-400" label="-" onClick={() => onDecrease(key)} />
		<Button
			style="rounded-tr-md rounded-br-md bg-yellow-400"
			label="0"
			onClick={() => onInitialize(key)}
		/>
	</div>

	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<span
		class="text-gray-500 p-1 cursor-pointer bg-cyan"
		on:click={() => onRemove(key)}
		role="button"
		tabindex="0">x</span
	>
</div>
