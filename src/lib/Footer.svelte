<script lang="ts">
	import Fa from 'svelte-fa';
	import { faCode } from '@fortawesome/free-solid-svg-icons';
</script>

<footer>
	<div class="poweredby">
		<div>
			Powered by <a href="https://kit.svelte.dev" target="_blank">SvelteKit</a> and
			<a href="https://svelte-cubed.vercel.app/" target="_blank">SvelteCubed</a>
		</div>
	</div>
	<div>
		<a class="btn" href="https://github.com/okletsgo-rivas/iamrivas.com" target="_blank">
			<Fa icon={faCode} size="lg" fw />
		</a>
	</div>
</footer>

<style>
	footer {
		position: absolute;
		left: 0;
		bottom: 10px;
		display: flex;
		width: 100%;
		padding: 0 1em;
		text-align: center;
		opacity: 0.5;
		pointer-events: all;
		font-size: small;
		box-sizing: border-box;
	}

	footer a {
		color: var(--accent-color);
		font-weight: bold;
	}

	.poweredby {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: flex-end;
		flex-grow: 1;
	}

	.btn {
		float: right;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #fff;
		width: 3em;
		height: 3em;
		background: rgba(0, 0, 0, 0.25);
		border-radius: 100%;
	}

	.btn:hover {
		background: rgba(0, 0, 0, 0.5);
	}
</style>
