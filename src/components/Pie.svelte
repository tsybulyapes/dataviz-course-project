<script>
	import { arc } from 'd3';

	export let width;
	export let height;
	export let arcs;

	const innerRadius = width / 5;

	const arcPath = arc()
		.innerRadius(innerRadius)
		.outerRadius(Math.min(width, height) / 2 - 10);
</script>

<div class="pie-chart">
	<h3>{arcs.name}</h3>
	<div class="pie-chart__content" bind:clientWidth={width} bind:clientHeight={height}>
		<svg {width} {height} viewBox="{-width / 2}, {-height / 2}, {width}, {height}">
			{#each arcs.pieChartData as segment}
				<path d={arcPath(segment)} fill={segment.data.fill} />
				<text x={-width / 8} y={height / 32} font-family="Unbounded" font-size="12" fill="white">
					{arcs.percentage}%
				</text>
			{/each}
		</svg>
	</div>
</div>

<style>
	.pie-chart {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.pie-chart__content {
		width: 100%;
		height: 100%;
		max-width: 200px;
		max-height: 200px;
	}

	h3 {
		font-size: 0.85rem;
		font-weight: 400;
		margin-bottom: 0px;
		margin-top: 20px;
		text-align: center;
	}
</style>
