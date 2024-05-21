<script>
	import { browser } from '$app/environment';

	if (browser) {
		// @ts-ignore
		const counts = document.querySelectorAll('.count');
		const speed = 150;

		counts.forEach((counter) => {
			function upDate() {
				const target = Number(counter.getAttribute('data-target'));
				const count = Number(counter.innerText);
				const inc = target / speed;
				if (count < target) {
					counter.innerText = Math.floor(inc + count);
					setTimeout(upDate, 15);
				} else {
					counter.innerText = target;
				}
			}
			upDate();
		});
	}

  // need to update the code
</script>

<main>
	<div class="back">
		<div class="counter-wrapper">
			<div class="counter">
				<h1 class="count" data-target="38980">0</h1>
				<p>повітряних тривог було оголошено<br />в Україні з 24 лютого 2022 року</p>
			</div>
		</div>
	</div>
</main>

<style>
	* {
		transition: 0.2s linear;
		-webkit-transition: 0.2s linear;
		-moz-transition: 0.2s linear;
		-ms-transition: 0.2s linear;
		-o-transition: 0.2s linear;
	}

	main {
		background-image: url(dmytro-tolokonov-g5rzXf74v5U-unsplash.jpg);
		opacity: 1;
		max-width: 100%;
		height: 100vh;
		max-height: 960px;
		overflow: hidden;
	}

	.back {
		background-color: rgba(0, 0, 0, 0.8);
		max-width: 100%;
		height: 100vh;
		max-height: 960px;
		overflow: hidden;
	}

	.count {
		font-size: 100px;
		font-family: 'Unbounded', sans-serif;
		font-weight: 700;
		color: white;
	}

	.counter-wrapper {
		background-size: cover;
		background-position: center;
		display: block;
		align-self: center;
		padding: 6rem 9%;
		position: relative;
	}
	.counter-wrapper::before {
		position: absolute;
		content: '';
		content: 0;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: 1;
	}
	.counter {
		text-align: center;
		color: white;
		z-index: 2;
		position: relative;
	}

	.counter .count {
		font-size: 8rem;
		margin-bottom: 1rem;
	}
	.counter p {
		font-size: 2rem;
		font-family: 'Unbounded', sans-serif;
		font-weight: 700;
		color: white;
	}
</style>
