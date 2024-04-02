# Neural Network Visualization with Activation Functions

This project is a simple web application built with SvelteKit and TypeScript that demonstrates how activation functions can affect the output of a neural network. It provides an interactive visualization of a basic neural network with one input neuron, one hidden layer with three neurons, and one output neuron.

## Features

- Adjust the input value (x) using a slider
- Select different activation functions (Sigmoid, Tanh, ReLU) for the hidden layer
- Observe the output of the neural network in real-time
- Visualize the output value over time using a line chart
- View the weights of the hidden layer neurons using a bar chart

## Prerequisites

Before running the application, make sure you have the following installed:

- Node.js (version 14 or above)
- npm (version 6 or above)

## Getting Started

1. Clone the repository:

```bash
git clone https://github.com/your-username/neural-network-visualization.git
```

2. Navigate to the project directory:

```bash
cd neural-network-visualization
```

3. Install the dependencies:

```bash
npm install
```

4. Start the development server:

```bash
npm run dev
```

5. Open your browser and visit `http://localhost:5173` (or the URL provided by SvelteKit) to see the application.

## Usage

- Use the slider to adjust the input value (x) and observe how it affects the output of the neural network.
- Select different activation functions from the dropdown menu to see how they influence the output.
- The line chart displays the output value over time, updating every second.
- The bar chart shows the weights of the hidden layer neurons.

## Customization

You can customize the neural network by modifying the following variables in the code:

- `weights`: An array of weights for the hidden layer neurons.
- `bias`: The bias value for the hidden layer.

Feel free to experiment with different weight values and observe their impact on the network's output.

## Dependencies

The project uses the following main dependencies:

- SvelteKit: A framework for building web applications with Svelte.
- TypeScript: A typed superset of JavaScript that compiles to plain JavaScript.
- Chart.js: A powerful charting library for creating interactive and responsive charts.
- Svelte-Chartjs: A Svelte wrapper for Chart.js, providing easy-to-use Svelte components for charts.
