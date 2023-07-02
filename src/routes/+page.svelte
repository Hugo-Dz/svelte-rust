<script lang="ts">
	// Svelte
	import { onMount } from "svelte";
	import { quintInOut } from "svelte/easing";
	import { scale } from "svelte/transition";

	// Libs
	import init, { add } from "$lib/pkg/my_package";
	// @ts-ignore
	import { Confetti } from "svelte-confetti";

	// Variables
	let numberA: number;
	let numberB: number;
	let result: number;
	let calculationMade: boolean = false;

	onMount(async () => {
		await init();
	});

	function handleClick(): void {
		calculationMade = true;
		result = add(numberA, numberB);
	}
</script>

<div class="flex px-4 w-full h-screen items-center justify-center flex-col">
	<!--Card-->
	<div
		class="relative flex flex-col justify-center items-center rounded-lg p-6 border border-slate-200 shadow-sm bg-white"
	>
		<!--Result container-->
		<div class="absolute -top-20">
			{#key result}
				{#if calculationMade}
					<div class="absolute top-0 left-1/2">
						<Confetti
							size="30"
							amount="8"
							x={[-0.5, 0.5]}
							colorArray={["url(/images/rust.svg)"]}
						/>
						<Confetti
							size="20"
							amount="5"
							x={[-0.75, -0.3]}
							y={[0.15, 0.75]}
							colorArray={["url(/images/rust.svg)"]}
						/>
						<Confetti
							size="10"
							amount="2"
							x={[0.3, 0.75]}
							y={[0.15, 0.75]}
							colorArray={["url(/images/rust.svg)"]}
						/>
					</div>
				{/if}
				<div
					class="px-4 py-2 text-center min-w-[120px] border border-slate-200 rounded-lg bg-white"
				>
					<p in:scale>{result ? result : "Result here"}</p>
				</div>
			{/key}
		</div>

		<!--Title container-->
		<div class="flex flow-row justify-center items-center space-x-3">
			<div
				class="border h-full flex items-center justify-center aspect-square sm:aspect-auto border-orange-600 rounded-lg p-2 bg-gradient-to-br from-slate-50 to-slate-200"
			>
				<img src="/images/rust.svg" alt="Rust" height="48" width="48" />
			</div>
			<div class="flex flex-col justify-center items-start w-full">
				<h1 class="font-medium text-lg text-slate-950">Rust in Svelte</h1>
				<p class="text-slate-500 font-light">
					Execute Rust code in your Svelte app
				</p>
			</div>
		</div>
		<!--Form container-->
		<form
			class="flex flex-col w-full justify-center space-y-6 mt-6 items-center"
		>
			<!--Inputs-->
			<div class="flex flex-col w-full justify-center space-y-3 items-center">
				<div class="flex flex-col w-full justify-center items-start space-y-2">
					<label for="a" class="text-slate-400 font-light">Number A</label>
					<input
						bind:value={numberA}
						type="number"
						name="a"
						id="a"
						class="rounded-md px-2 focus:outline-none py-2 w-full border border-slate-200"
					/>
				</div>
				<div class="flex flex-col w-full justify-center items-start space-y-2">
					<label for="b" class="text-slate-400 font-light">Number B</label>
					<input
						bind:value={numberB}
						type="number"
						name="b"
						id="b"
						class="rounded-md focus:outline-none px-2 w-full py-2 border border-slate-200"
					/>
				</div>
			</div>
			<button
				on:click|preventDefault={handleClick}
				class="py-3 shadow rounded-md bg-gradient-to-b from-orange-500 to-orange-600 text-white w-full font-medium"
			>
				<p>Calculate A + B</p>
			</button>
		</form>
	</div>
	<!--Credits-->

</div>
