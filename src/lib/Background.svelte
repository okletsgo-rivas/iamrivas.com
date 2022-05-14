<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	import { onMount } from 'svelte';
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';

	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import type { Position } from 'svelte-cubed/types/common';
	import type { Texture } from 'three';

	let spinY = 0;
	let spinZ = 0;
	let coin = new THREE.TextureLoader();

	const progress = tweened(0, {
		duration: 500,
		easing: cubicOut
	});

	SC.onFrame(() => {
		spinY = (spinY + spinSpeed) % ((360 * Math.PI) / 180);
	});
	let blockArr: any = [0, 1]
		.map((i) =>
			[0, 1].map((j) =>
				[0, 1].map((k) => ({
					path: [i, j, k],
					position: [0, 0, 0] as Position,
					color: (i + j + k) % 2 ? 0xffffff : 0x222222
				}))
			)
		)
		.flat(2);

	let planeTexture: Texture;
	let cameraPostion: number[] = [1, 1.5, 3];
	// let projector = new THREE.Projector();
	let mouse = { x: 0, y: 0, z: 1 };
	let intersects: boolean;
	let ray = new THREE.Raycaster(new THREE.Vector3(0, 0, 0), new THREE.Vector3(0, 0, 0));
	const camera_vector = new THREE.Vector3(1, 0, 3);
	const mouse_vector = new THREE.Vector3();

	const box = new THREE.BoxGeometry();
	const mesh = new THREE.Mesh(box);
	// box.translate(0.5, 0.25, 0);
	mesh.position.set(0.5, 0.25, 0);

	// $: mesh.rotation.y = (spin * Math.PI) / 180;
	$: scale = $progress * -0.45 + 0.5;
	$: spinZ = intersects ? spinY / 2 : 0;
	$: $progress = intersects ? 1 : 0;
	$: spinSpeed = (intersects ? 5 : 0.5) * (Math.PI / 180);
	$: {
		const factor = $progress * 0.25 + 0.25;
		blockArr.map((block: any, i: number) => {
			blockArr[i].position = block.path.map((val: number) => factor * (val ? 1 : -1));
		});
	}

	function onMouseMove(e: MouseEvent) {
		e.preventDefault();

		mouse = {
			x: (e.clientX / window.innerWidth) * 2 - 1,
			y: (e.clientY / window.innerHeight) * 2 - 1,
			z: 1
		};
		mouse_vector.set(mouse.x, mouse.y, mouse.z);
		const direction = mouse_vector.sub(camera_vector).normalize();
		ray.set(camera_vector, direction);
		intersects = !!ray.intersectObject(mesh).length;
	}

	onMount(() => {
		planeTexture = new THREE.TextureLoader().load('bg.gif');
		planeTexture.wrapS = THREE.RepeatWrapping;
		planeTexture.wrapT = THREE.RepeatWrapping;
		planeTexture.repeat.set(50, 50);
	});
</script>

<svelte:body on:mousemove={onMouseMove} />

<SC.Canvas
	antialias
	background={new THREE.Color(0xd9e5e7)}
	fog={new THREE.FogExp2(0xd9e5e7, 0.1)}
	shadows
>
	<SC.Group position={[0, -0.5, 0]}>
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

	<SC.Group position={[0.5, 0.25, 0]}>
		<SC.Mesh
			geometry={new THREE.PlaneGeometry(1, 1)}
			material={new THREE.MeshBasicMaterial({
				transparent: true,
				map: coin.load('profile.jpg')
			})}
			scale={0.5}
			rotation={[0, 0, 0]}
			receiveShadow
		/>
	</SC.Group>

	<!-- Test Hitbox
	<SC.Mesh
		geometry={box}
		castShadow
		position={[mesh.position.x, mesh.position.y, mesh.position.z]}
		rotation={[0, spin, 0]}
	/> -->

	<SC.Group position={[0.5, 0.4, 0]} rotation={[0, spinY, spinZ]}>
		{#each blockArr as block}
			<SC.Mesh
				geometry={new THREE.BoxGeometry()}
				material={new THREE.MeshStandardMaterial({
					color: block.color
				})}
				position={block.position}
				scale={[scale, scale, scale]}
				castShadow
			/>
		{/each}
	</SC.Group>

	<SC.PerspectiveCamera bind:position={cameraPostion} />
	<SC.AmbientLight intensity={0.9} />
	<SC.DirectionalLight intensity={0.1} position={[4, 3, 1]} shadow={{ mapSize: [2048, 2048] }} />
</SC.Canvas>
