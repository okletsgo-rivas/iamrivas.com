<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import type { Position } from 'svelte-cubed/types/common';
	import { onMount } from 'svelte';
	import type { Texture } from 'three';

	let spin = 0;
	let links = [
		{
			title: 'By Framework',
			links: [
				{ href: 'http://js.iamrivas.com/', title: 'Vanilla JS', enabled: false },
				{ href: 'http://react.iamrivas.com/', title: 'React', enabled: true },
				{ href: 'http://vue.iamrivas.com/', title: 'Vue', enabled: false },
				{ href: 'http://svelte.iamrivas.com/', title: 'Svelte', enabled: false },
				{ href: 'http://ng.iamrivas.com/', title: 'Angular', enabled: false },
				{ href: 'http://d8.iamrivas.com/', title: 'Drupal', enabled: true }
			]
		},
		{
			title: 'By SSR stack',
			links: [
				{ href: 'http://sveltekit.iamrivas.com/', title: 'SveltKit', enabled: false },
				{ href: 'http://gatsby.iamrivas.com/', title: 'React / Drupal / Gatsby', enabled: true }
			]
		}
	];

	SC.onFrame(() => {
		spin += 0.01;
	});

	let planeTexture: Texture;

	function getPosition(arr: number[]): Position {
		return arr.map((_) => 0.25 * (_ ? 1 : -1)) as Position;
	}

	onMount(() => {
		planeTexture = new THREE.TextureLoader().load('bg.gif');
		planeTexture.wrapS = THREE.RepeatWrapping;
		planeTexture.wrapT = THREE.RepeatWrapping;
		planeTexture.repeat.set(50, 50);
	});
</script>

<svelte:head>
	<title>i am RIVAS: Home Page</title>
	<meta name="description" content="John Rivas Portfolio" />
</svelte:head>

<SC.Canvas
	antialias
	background={new THREE.Color(0xd9e5e7)}
	fog={new THREE.FogExp2(0xd9e5e7, 0.1)}
	shadows
>
	<SC.Group position={[0, -1 / 2, 0]}>
		<SC.Mesh
			geometry={new THREE.PlaneGeometry(50, 50)}
			material={new THREE.MeshStandardMaterial({
				color: 0xffffff,
				map: planeTexture
			})}
			rotation={[-Math.PI / 2, 0, 0]}
			receiveShadow
		/>
	</SC.Group>

	<SC.Group position={[0.5, 0, 0]} rotation={[0, spin, 0]}>
		{#each [0, 1] as i}
			{#each [0, 1] as j}
				{#each [0, 1] as k}
					<SC.Mesh
						geometry={new THREE.BoxGeometry()}
						material={new THREE.MeshStandardMaterial({
							color: (i + j + k) % 2 ? 0xffffff : 0x222222
						})}
						position={getPosition([i, j, k])}
						scale={[0.5, 0.5, 0.5]}
						castShadow
					/>
				{/each}
			{/each}
		{/each}
	</SC.Group>

	<SC.PerspectiveCamera position={[1, 1, 3]} />
	<SC.OrbitControls enableZoom={false} maxPolarAngle={Math.PI * 0.51} />
	<SC.AmbientLight intensity={0.6} />
	<SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} shadow={{ mapSize: [2048, 2048] }} />
</SC.Canvas>
<section>
	<div style="padding:1rem;background:rgba(255,255,255,0.5)">
		<h1 style="margin-top:0.5rem">Portfolio</h1>
		{#each links as group}
			<strong>{group.title}</strong>
			<ul style="margin:0.5rem 0 2rem 0">
				{#each group.links as link}
					<li>
						<a href={link.href} target="_blank" class:disable={!link.enabled}>{link.title}</a>
					</li>
				{/each}
			</ul>
		{/each}
	</div>
</section>

<style>
	section {
		position: absolute;
		top: 100px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	a {
		color: #666;
		text-decoration: underline;
	}
	a:hover {
		color: #000;
	}

	.disable {
		color: #ccc;
		pointer-events: none;
		text-decoration: line-through;
	}
</style>
