<script lang="ts">
	// import { page } from '$app/stores';
	import Fa from 'svelte-fa';
	import { faGithub, faLinkedin, faPinterest } from '@fortawesome/free-brands-svg-icons';

	import logo from './logo.svg';

	const portLinks = [
		{
			title: 'View with Framework',
			links: [
				{ href: 'https://js.iamrivas.com/', title: 'Vanilla JS', enabled: false },
				{ href: 'https://react.iamrivas.com/', title: 'React', enabled: true },
				{ href: 'https://vue.iamrivas.com/', title: 'Vue', enabled: false },
				{ href: 'https://svelte.iamrivas.com/', title: 'Svelte', enabled: false },
				{ href: 'https://ng.iamrivas.com/', title: 'Angular', enabled: true },
				{ href: 'https://d9.iamrivas.com/', title: 'Drupal', enabled: true }
			]
		},
		{
			title: 'View with SSR stack',
			links: [
				{ href: 'http://sveltekit.iamrivas.com/', title: 'SveltKit', enabled: false },
				{ href: 'http://gatsby.iamrivas.com/', title: 'React / Drupal / Gatsby', enabled: true }
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
			<strong>{group.title}</strong>
			<ul style="margin:0.5rem 0 2rem 0">
				{#each group.links as link}
					<li>
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
		padding: 1rem;
		background: rgba(255, 255, 255, 0.5);
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
