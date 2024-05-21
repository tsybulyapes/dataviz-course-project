<script>
	import {
		json,
		geoMercator,
		geoPath,
		groups,
		scaleLinear,
		extent,
		line,
		curveMonotoneX,
		curveNatural
	} from 'd3';
	import csv from './data_graph_1.csv';

	const colors = {
		2022: '#E30101',
		2023: '#ff6d00',
		2024: '#ffffff'
	};

	const lineGenerator = line()
		.x((d) => d.x)
		.y((d) => d.y)
		.curve(curveMonotoneX);

	let width = 0;
	let height = 0;

	// const legendHeight = 250;

	let margin = {
		top: 40,
		left: 60,
		right: 100,
		bottom: 0
	};

	$: chartWidth = width - margin.left - margin.right;
	$: chartHeight = height - margin.top - margin.bottom;

	$: oblData = csv.map((el) => {
		return {
			year: parseInt(el.year),
			month: parseInt(el.month),
			strike_count: parseInt(el.strike_count)
		};
	});

	$: xScale = scaleLinear()
		.domain(extent(oblData, (d) => d.month))
		.range([margin.left, chartWidth]);

	$: yScale = scaleLinear()
		.domain(extent(oblData, (d) => d.strike_count))
		.range([chartHeight, margin.top]);

	let dataByYear = [];
	$: groups(oblData, (d) => d.year).forEach((el) => {
		dataByYear.push({
			year: el[0],
			values: el[1]
		});
	});

	$: renderedData = dataByYear.map((el) => {
		const renderedValues = el.values.map((mon) => {
			return {
				...mon,
				x: xScale(mon.month),
				y: yScale(mon.strike_count)
			};
		});

		return {
			...el,
			values: renderedValues,
			path: lineGenerator(renderedValues),
			stroke: colors[el.year],
			strokeWidth: 4.0,
			opacity: 1.0
		};
	});

	function parseMonth(monthNum) {
		const monthesMap = new Map([
			[1, 'Січ'],
			[2, 'Лют'],
			[3, 'Бер'],
			[4, 'Кві'],
			[5, 'Тра'],
			[6, 'Чер'],
			[7, 'Лип'],
			[8, 'Сер'],
			[9, 'Вер'],
			[10, 'Жов'],
			[11, 'Лис'],
			[12, 'Гру']
		]);

		return monthesMap.get(monthNum);
	}
</script>

<div class="wrap">
	<div class="head">
		<h1>Графік кількості повітряних тривог</h1>
		<p class="date">За кожен рік повномасштабного вторгненя</p>
	</div>
	<!-- svelte-ignore a11y-no-static-element-interactions -->

	<main bind:clientWidth={width} bind:clientHeight={height}>
		<svg {width} {height}>
			<g class="axis">
				{#each yScale.ticks(10) as tick}
					<line
						x1={margin.left - 10}
						y1={yScale(tick)}
						x2={margin.left}
						y2={yScale(tick)}
						stroke="white"
						stroke-width={2}
					/>
				{/each}
			</g>

			<g class="axis">
				{#each yScale.ticks(10) as tick}
					<line
						x1={margin.left}
						y1={yScale(tick)}
						x2={chartWidth}
						y2={yScale(tick)}
						stroke="white"
						stroke-width={0.2}
					/>
					<text x={margin.left - 40} y={yScale(tick) + 6} text-anchor="middle" fill="white"
						>{tick}</text
					>
				{/each}
			</g>

			<g class="axis">
				{#each xScale.ticks(width > 800 ? 12 : 4) as tick}
					<line
						x1={xScale(tick)}
						y1={chartHeight}
						x2={xScale(tick)}
						y2={chartHeight + 10}
						stroke="white"
						stroke-width={2}
					/>
					<text x={xScale(tick)} y={chartHeight + 30} text-anchor="middle" fill="white"
						>{parseMonth(tick)}</text
					>
				{/each}
			</g>

			{#each renderedData as { path, stroke, strokeWidth, opacity }}
				<path d={path} {stroke} stroke-width={strokeWidth} {opacity} />
			{/each}

			<line
				x1={margin.left}
				y1={chartHeight}
				x2={chartWidth}
				y2={chartHeight}
				stroke="white"
				stroke-width={2}
			/>

			<line
				x1={margin.left}
				y1={margin.top}
				x2={margin.left}
				y2={chartHeight}
				stroke="white"
				stroke-width={2}
			/>
		</svg>

		<div class="legend">
			<ul>
				<li><span style={`background: #E30101`}></span>2022</li>
				<li><span style={`background: #ff6d00`}></span>2023</li>
				<li><span style={`background: #ffffff`}></span>2024</li>
			</ul>
		</div>
	</main>
</div>

<style>
	.wrap {
		font-family: 'Unbounded', sans-serif;
		margin-top: 15rem;
		font-size: 0.85rem;
		font-family: 'Unbounded', sans-serif;
		color: white;
	}

	main {
		position: relative;
		width: 100%;
		height: 600px;
		background-color: black;
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	.head {
		max-width: 900px;
		width: 100%;
		margin: 0 auto;
		color: #fff;
	}

	svg {
		width: 100%;
		height: 100%;
	}

	.date {
		font-weight: 300;
		font-size: 1rem;
		margin-top: -1%;
	}

	path {
		fill: transparent;
		stroke-linecap: round;
	}

	.legend ul {
		margin: 0;
		padding: 0;
	}

	.legend ul li {
		list-style: none;
		display: flex;
		align-items: center;
		margin: 5px 0;
	}

	.legend ul li span {
		width: 80px;
		height: 4px;
		margin-right: 10px;
		border-radius: 3px;
	}
</style>
