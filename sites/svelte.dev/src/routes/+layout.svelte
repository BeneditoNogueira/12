<script>
	import '@sveltejs/site-kit/base.css';
	import { page, navigating } from '$app/stores';
	import { Icon, Icons, Nav, NavItem, SkipLink } from '@sveltejs/site-kit';
	import PreloadingIndicator from '$lib/components/PreloadingIndicator.svelte';
	import StopWar from './stopwar.svg';
</script>

<Icons />

{#if $navigating && $navigating.to}
	<PreloadingIndicator />
{/if}

{#if $page.url.pathname !== '/repl/embed'}
	<SkipLink href="#main" />
	<Nav {page} logo={StopWar}>
		<svelte:fragment slot="nav-center">
			<NavItem href="/tutorial">Tutorial</NavItem>
			<NavItem href="/docs">Docs</NavItem>
			<NavItem href="/examples">Examples</NavItem>
			<NavItem href="/repl">REPL</NavItem>
			<NavItem href="/blog">Blog</NavItem>
			<NavItem href="/faq">FAQ</NavItem>
		</svelte:fragment>

		<svelte:fragment slot="nav-right">
			<NavItem external="https://kit.svelte.dev">SvelteKit</NavItem>

			<NavItem external="/chat" title="Discord Chat">
				<span class="small">Discord</span>
				<span class="large"><Icon name="message-square" /></span>
			</NavItem>

			<NavItem external="https://github.com/sveltejs/svelte" title="GitHub Repo">
				<span class="small">GitHub</span>
				<span class="large"><Icon name="github" /></span>
			</NavItem>
		</svelte:fragment>
	</Nav>
{/if}

<svelte:head>
	{#if $page.route.id !== '/blog/[slug]'}
		<meta name="twitter:card" content="summary" />
		<meta name="twitter:image" content="https://svelte.dev/images/twitter-thumbnail.jpg" />
		<meta name="og:image" content="https://svelte.dev/images/twitter-thumbnail.jpg" />
	{/if}
</svelte:head>

<main id="main">
	<slot />
</main>

<style>
	@media (max-width: 830px) {
		:global(aside) {
			z-index: 9999 !important;
		}
	}

	main {
		position: relative;
		margin: 0 auto;
		/* padding: var(--nav-h) var(--side-nav) 0 var(--side-nav); */
		padding: var(--nav-h) 0 0 0;
		overflow: auto;
	}

	.small {
		display: inline;
	}

	.large {
		display: none;
	}

	@media (min-width: 800px) {
		.small {
			display: none;
		}

		.large {
			display: inline;
		}
	}

	:global(.examples-container, .repl-outer, .tutorial-outer) {
		height: calc(100vh - var(--nav-h)) !important;
	}

	:global(.toggle) {
		bottom: 0 !important;
	}

	:global(.zen-mode) {
		height: 100vh !important;
	}

	@media (max-width: 830px) {
		:global(aside) {
			z-index: 9999 !important;
		}
	}
</style>
