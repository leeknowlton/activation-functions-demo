<script lang="ts">
	import { Line, Bar } from 'svelte-chartjs';
	import { onMount } from 'svelte';
	import {
		Chart,
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		PointElement,
		CategoryScale,
		BarElement
	} from 'chart.js';

	Chart.register(
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		PointElement,
		CategoryScale,
		BarElement
	);

	let x: number = 0;
	let activationFunction: 'sigmoid' | 'tanh' | 'relu' = 'sigmoid';
	let chartData: number[] = [];
	let chartLabels: string[] = [];

	function sigmoid(x: number): number {
		return 1 / (1 + Math.exp(-x));
	}

	function tanh(x: number): number {
		return Math.tanh(x);
	}

	function relu(x: number): number {
		return Math.max(0, x);
	}

	function calculateOutput(
		x: number,
		weights: number[],
		bias: number,
		activationFunction: 'sigmoid' | 'tanh' | 'relu'
	): number {
		const sum = weights.reduce((acc, weight, i) => acc + weight * x, bias);
		return activationFunction === 'sigmoid'
			? sigmoid(sum)
			: activationFunction === 'tanh'
				? tanh(sum)
				: relu(sum);
	}

	let weights: number[] = [0.5, -0.8, 1.2];
	let bias: number = 0.3;
	$: output = calculateOutput(x, weights, bias, activationFunction);

	onMount(() => {
		const interval = setInterval(() => {
			chartData = [...chartData, output];
			chartLabels = [...chartLabels, new Date().toLocaleTimeString()];
			if (chartData.length > 10) {
				chartData.shift();
				chartLabels.shift();
			}
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>

<main>
	<h1>Neural Network with Activation Functions</h1>

	<label>
		Input (x):
		<input type="range" min="-10" max="10" step="0.1" bind:value={x} />
		{x.toFixed(1)}
	</label>

	<div>
		<label>
			Activation Function:
			<select bind:value={activationFunction}>
				<option value="sigmoid">Sigmoid</option>
				<option value="tanh">Tanh</option>
				<option value="relu">ReLU</option>
			</select>
		</label>
	</div>

	<div>
		<h2>Output</h2>
		<p>{output.toFixed(4)}</p>
	</div>

	<div>
		<h2>Output Over Time</h2>
		<Line
			data={{
				labels: chartLabels,
				datasets: [
					{
						label: 'Output',
						data: chartData,
						borderColor: 'blue',
						fill: false
					}
				]
			}}
			options={{
				responsive: true,
				scales: {
					x: {
						display: true,
						title: {
							display: true,
							text: 'Time'
						}
					},
					y: {
						display: true,
						title: {
							display: true,
							text: 'Output'
						}
					}
				}
			}}
		/>
	</div>

	<div>
		<h2>Neuron Weights</h2>
		<Bar
			data={{
				labels: weights.map((_, i) => `Neuron ${i + 1}`),
				datasets: [
					{
						label: 'Weight',
						data: weights,
						backgroundColor: 'rgba(75, 192, 192, 0.6)'
					}
				]
			}}
			options={{
				responsive: true,
				scales: {
					y: {
						beginAtZero: true
					}
				}
			}}
		/>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 20px;
	}
</style>
