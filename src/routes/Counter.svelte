<script lang="ts">
	let button = $state<HTMLButtonElement>();
	let star = $state<SVGElement>();

	let count = $state(0);

	var colors = [
		'#ffb3f6',
		'#FFD100',
		'#FF9300',
		'#FF7FA4',
		'#7aa0ff',
		// '#333',
	];

	function onClick(e: MouseEvent) {
		count += 1;

		const num = 5;

		for (let i = 0; i < num; i++) {
			const r = Math.random() * 150 + 70;
			const theta = Math.random() * 2 * Math.PI;
			const x = r * Math.cos(theta);
			const y = r * Math.sin(theta);

			const el = star!.cloneNode(true) as SVGElement;

			el.style.fill = colors[Math.floor(Math.random() * colors.length)];
			el.style.width = Math.floor(Math.random() * 20 + 5) + 'px';

			const animation = el.animate(
				[{ transform: `scale(0) translate(${x}px, ${y}px)` }],
				{ duration: 1000 },
			);

			animation.onfinish = () => button!.removeChild(el);

			button!.appendChild(el);
		}
	}
</script>

<div class="counter">
	<span>{count}</span>

	<button bind:this={button} on:click={onClick}>Add</button>

	<div style="display: none">
		<svg bind:this={star} class="star" viewBox="0 0 47.94 47.94">
			<path
				d="M26.285,2.486l5.407,10.956c0.376,0.762,1.103,1.29,1.944,1.412l12.091,1.757 c2.118,0.308,2.963,2.91,1.431,4.403l-8.749,8.528c-0.608,0.593-0.886,1.448-0.742,2.285l2.065,12.042 c0.362,2.109-1.852,3.717-3.746,2.722l-10.814-5.685c-0.752-0.395-1.651-0.395-2.403,0l-10.814,5.685 c-1.894,0.996-4.108-0.613-3.746-2.722l2.065-12.042c0.144-0.837-0.134-1.692-0.742-2.285l-8.749-8.528 c-1.532-1.494-0.687-4.096,1.431-4.403l12.091-1.757c0.841-0.122,1.568-0.65,1.944-1.412l5.407-10.956 C22.602,0.567,25.338,0.567,26.285,2.486z"
			></path>
		</svg>
	</div>
</div>

<style>
	button {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.star {
		position: absolute;
		user-select: none;
		z-index: -1;
	}
</style>
