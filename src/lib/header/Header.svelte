<script lang="ts">
	// import { page } from '$app/stores';
	import Fa from 'svelte-fa';
	import {
		faGithub,
		faLinkedin,
		faPinterest,
		faReact,
		faJs,
		faVuejs,
		faAngular,
		faDrupal
	} from '@fortawesome/free-brands-svg-icons';

	import logo from './logo.svg';

	const portLinks = [
		{
			title: 'View with Framework',
			links: [
				{
					href: 'https://svelte.iamrivas.com/',
					title: 'Svelte (WIP)',
					icon: faJs,
					iconColor: '#F5B21B',
					enabled: false
				},
				{
					href: 'https://react.iamrivas.com/',
					title: 'React',
					icon: faReact,
					iconColor: '#60D8FB',
					enabled: true
				},
				{
					href: 'http://vue.iamrivas.com/',
					title: 'Vue',
					icon: faVuejs,
					iconColor: '#40B783',
					enabled: true
				},
				{
					href: 'https://ng.iamrivas.com/',
					title: 'Angular',
					icon: faAngular,
					iconColor: '#D82C31',
					enabled: true
				},
				{
					href: 'https://js.iamrivas.com/',
					title: 'Vanilla JS (WIP)',
					icon: faJs,
					iconColor: '#F5B21B',
					enabled: false
				},
				{
					href: 'https://d9.iamrivas.com/',
					title: 'Drupal (WIP)',
					icon: faDrupal,
					iconColor: '#098ACE',
					enabled: true
				}
			]
		},
		{
			title: 'View with SSR stack',
			links: [
				{
					href: 'http://sveltekit.iamrivas.com/',
					title: 'SveltKit',
					icon: faJs,
					iconColor: '#F5B21B',
					enabled: false
				},
				{
					href: 'http://gatsby.iamrivas.com/',
					title: 'React/Drupal/Gatsby (WIP)',
					icon: faJs,
					iconColor: '#F5B21B',
					enabled: true
				}
			]
		}
	];

	const socialLinks = [
		{
			title: 'Github',
			icon: faGithub,
			href: 'https://github.com/okletsgo-rivas'
		},
		{
			title: 'LinkedIn',
			icon: faLinkedin,
			href: 'https://www.linkedin.com/in/johnrivas/'
		},
		{
			title: 'Pinterest',
			icon: faPinterest,
			href: 'https://www.pinterest.com/johnrivas714'
		}
	];
</script>

<header>
	<div class="corner">
		{#each socialLinks as link}
			<a href={link.href} target="_blank">
				<Fa icon={link.icon} size="2x" />
			</a>
		{/each}
	</div>

	<img src={logo} alt="SvelteKit" style="width:auto;height:50px" />
	<br />
	<br />

	<nav>
		<h1 style="margin-top:0.5rem">Portfolio</h1>
		{#each portLinks as group}
			<strong style="color:#666">{group.title}</strong>
			<ul style="margin:0.5rem 0 2rem 0;padding:0;list-style:none">
				{#each group.links as link}
					<li style="margin-bottom:0.5rem">
						<Fa icon={link.icon} size="lg" fw color={link.iconColor} />
						<a href={link.href} target="_blank" class:disable={!link.enabled}>{link.title}</a>
					</li>
				{/each}
			</ul>
		{/each}
	</nav>
</header>

<style>
	header {
		width: 100%;
	}

	.corner {
		margin-top: 1em;
		float: right;
		pointer-events: all;
	}

	.corner a {
		margin-left: 1em;
	}
	nav {
		display: inline-block;
		padding: 1.5rem;
		background: rgba(255, 255, 255, 0.4);
		pointer-events: all;
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
