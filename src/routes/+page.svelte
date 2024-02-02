<script lang="ts">
	import Button from '$components/Button.svelte';
	import Counter from '$components/Counter.svelte';

	// Define a type for each counter
	interface CounterType {
		title: string;
		value: number;
	}

	// Initialize counterArr array with one default counter
	let counterArr: CounterType[] = [{ title: 'New', value: 0 }];

	// Function to add a new counter to the counterArr array
	const addCounter = () => {
		counterArr = [...counterArr, { title: 'New', value: 0 }];
	};

	// Function to remove a counter from the counterArr array by index
	const removeCounter = (index: number) => {
		counterArr = counterArr.filter((_, currentIndex) => currentIndex !== index);
	};

	// Function to increase the value of a counter by 1
	const increaseCount = (index: number) => {
		counterArr[index].value += 1;
	};

	// Function to decrease the value of a counter by 1, if possible
	const decreaseCount = (index: number) => {
		if (counterArr[index].value - 1 >= 0) {
			counterArr[index].value -= 1;
		}
	};

	// Function to initialize the value of a counter to 0
	const initCount = (index: number) => {
		counterArr[index].value = 0;
	};

	// Reactive declaration to update when counterArr change
	$: titleList = counterArr.map((counter) => counter.title).join(', ');
	$: sumOfCount = counterArr.reduce((sum, counter) => sum + counter.value, 0);
</script>

<svelte:head>
	<title>Multiple Counter</title>
	<meta name="description" content="Multiple counter" />
</svelte:head>

<section class="flex flex-col w-full justify-start items-center">
	<div class="flex flex-col items-center gap-2">
		<h1 class="text-center text-6xl mb-10">Multiple Counter</h1>

		<div class="flex flex-col gap-2 items-center mb-5">
			{#each counterArr as counter, index}
				<Counter
					key={index}
					bind:counter
					onIncrease={() => increaseCount(index)}
					onDecrease={() => decreaseCount(index)}
					onInitialize={() => initCount(index)}
					onRemove={() => removeCounter(index)}
				/>
			{/each}
		</div>

		<!-- Button to add a new counter -->
		<Button label="New Counter" onClick={addCounter} style="w-full rounded-lg bg-green-400" />

		<!-- Display title list and sum of count -->
		<div class="flex flex-row gap-2">
			<span class="text-gray-700">Title list: {titleList}</span>
		</div>
		<div class="flex flex-row gap-2">
			<span class="text-gray-700">Sum of count: {sumOfCount}</span>
		</div>
	</div>
</section>
