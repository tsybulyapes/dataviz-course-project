<script>
	import PieChart from '../components/PieChart.svelte';
	import BarChart from '../components/BarChart.svelte';
	import Counter from '../components/Counter.svelte';
	import Graph_1 from '../components/Graph_1.svelte';
	import MapUa from '../components/MapUA.svelte';
	import ScatterPlot from '../components/ScatterPlot.svelte';
	import Text from '../components/Text.svelte';
	import Footer from '../components/Footer.svelte';
  import CounterV2 from '../components/CounterV2.svelte';
</script>

<main>
	<Counter />
  <CounterV2 text={'Bla bla'} start={10000}/>
	<div class="center">
		<Text />
		<MapUa />
		<Graph_1 />
		<ScatterPlot />
		<BarChart />
		<PieChart />
		<Footer />
	</div>
</main>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		background-color: black;
		overflow-x: hidden;
	}

	main {
		width: 100vw;
		height: 100%;
	}

	.center {
		width: 100%;
		max-width: 1140px;
		margin: 0 auto;
		padding: 0 15px;
	}
</style>
