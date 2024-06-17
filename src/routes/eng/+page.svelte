<script>
	import PieChart from '../../components/PieChart.svelte';
	import BarChart from '../../components/BarChart.svelte';
	import Graph_1 from '../../components/Graph_1.svelte';
	import MapUa from '../../components/MapUA.svelte';
	import ScatterPlot from '../../components/ScatterPlot.svelte';
	import Text from '../../components/Text.svelte';
	import Footer from '../../components/Footer.svelte';
  import CounterV2 from '../../components/Header/CounterV2.svelte';
  import Header from '../../components/Header/Header.svelte';

  let introText = [
    'English version of the text',
    'Second paragraph is here'
  ]

  let headLine = 'air alerts were announced<br />in Ukraine since February 24, 2022'

  let footerText = [
    "Lorem ipsum",
		"Created by: <strong>Катерина Березіна.</strong><br />",
    "Data source: <a href='https://github.com/Vadimkin/ukrainian-air-raid-sirens-dataset?tab=readme-ov-file' target='_blank'>Дані повітряних тривог в Україні під час повномасштабного вторгнення рф</a>",
    "<span class='slava'>Слава Україні!</span>"
  ]
</script>

<main>
  <Header headline={headLine}/>
	
	<div class="center">
		<Text text={introText}/>
		<MapUa 
      lang="eng"
      title="Number of air raid alerts by regions"
      legendTitle="Alerts Total"
    />
		<Graph_1 lang="eng"/>
		<ScatterPlot lang="eng"/>
		<BarChart  lang="eng"/>
		<PieChart lang="eng"/>
		<Footer content={footerText}/>
	</div>
</main>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		background-color: black;
	}


	main {
		height: 100%;
    overflow-x: hidden;
    
	}

	.center {
		width: calc(100% - 50px);
		max-width: 1140px;
		margin: 0 auto;
		padding: 0 25px;
    position: relative;
	}
</style>
