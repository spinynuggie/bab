<script lang="ts">
	import { resolve } from '$app/paths';
	import { page } from '$app/state';
	import { cubicOut } from 'svelte/easing';
	import { prefersReducedMotion, Tween } from 'svelte/motion';
	import { onMount } from 'svelte';
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
	let previousPath = $state(page.url.pathname);
	let headerProgress = $state(0);

	const routeProgress = new Tween(1, {
		duration: 720,
		easing: cubicOut
	});

	const navItems = [
		{ href: '/', label: 'Home' },
		{ href: '/over-ons', label: 'Over ons' },
		{ href: '/ik-zoek-hulp', label: 'Ik zoek hulp' },
		{ href: '/begeleiding-coaching', label: 'Begeleiding' },
		{ href: '/zorg-ondersteuning', label: 'Zorg' },
		{ href: '/contact', label: 'Contact' }
	] as const;

	const isActive = (href: string) =>
		href === '/' ? page.url.pathname === '/' : page.url.pathname === href;

	const clamp = (value: number) => Math.min(1, Math.max(0, value));
	const mix = (from: number, to: number, amount: number) => Math.round(from + (to - from) * amount);
	const headerColor = $derived(
		page.url.pathname === '/'
			? `rgb(${mix(255, 24, headerProgress)}, ${mix(255, 49, headerProgress)}, ${mix(255, 46, headerProgress)})`
			: 'rgb(24, 49, 46)'
	);
	const headerLine = $derived(
		page.url.pathname === '/'
			? `rgba(24, 49, 46, ${headerProgress * 0.14})`
			: 'rgba(35, 70, 63, 0.14)'
	);
	const headerBgOpacity = $derived(
		page.url.pathname === '/' ? Math.max(0, (headerProgress - 0.72) / 0.28) : 1
	);

	$effect(() => {
		const currentPath = page.url.pathname;

		if (currentPath === previousPath) {
			return;
		}

		previousPath = currentPath;
		headerProgress =
			currentPath === '/' && typeof window !== 'undefined'
				? clamp(window.scrollY / Math.min(window.innerHeight * 0.72, 620))
				: 1;

		if (prefersReducedMotion.current) {
			routeProgress.set(1, { duration: 0 });
			return;
		}

		routeProgress.set(0, { duration: 0 });
		routeProgress.set(1, { duration: 780, easing: cubicOut });
	});

	onMount(() => {
		let frame = 0;

		const updateHeaderProgress = () => {
			frame = 0;
			headerProgress =
				page.url.pathname === '/'
					? clamp(window.scrollY / Math.min(window.innerHeight * 0.72, 620))
					: 1;
		};

		const scheduleHeaderProgress = () => {
			if (frame) return;
			frame = requestAnimationFrame(updateHeaderProgress);
		};

		scheduleHeaderProgress();
		window.addEventListener('scroll', scheduleHeaderProgress, { passive: true });
		window.addEventListener('resize', scheduleHeaderProgress);

		return () => {
			if (frame) cancelAnimationFrame(frame);
			window.removeEventListener('scroll', scheduleHeaderProgress);
			window.removeEventListener('resize', scheduleHeaderProgress);
		};
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=Lora:wght@400;500;600;700&family=Source+Sans+3:wght@400;500;600;700;800&display=swap"
		rel="stylesheet"
	/>
	<title>Samenbijeen | Persoonlijke zorg en begeleiding</title>
	<meta
		name="description"
		content="Samenbijeen verbindt mensen met een zorgvraag aan betrokken professionals voor begeleiding, coaching en ondersteuning."
	/>
</svelte:head>

<div
	class="site-shell"
	class:home-shell={page.url.pathname === '/'}
	style:--header-color={headerColor}
	style:--header-line={headerLine}
	style:--header-bg-opacity={headerBgOpacity}
>
	<header class="site-header">
		<a class="brand" href={resolve('/')} aria-label="Samenbijeen home">
			<strong>Samenbijeen</strong>
		</a>

		<nav class="desktop-nav" aria-label="Hoofdnavigatie">
			{#each navItems as item (item.href)}
				<a class:active={isActive(item.href)} href={resolve(item.href)}>{item.label}</a>
			{/each}
		</nav>
	</header>

	<nav class="mobile-nav" aria-label="Mobiele navigatie">
		{#each navItems as item (item.href)}
			<a class:active={isActive(item.href)} href={resolve(item.href)}>{item.label}</a>
		{/each}
	</nav>

	<main
		style:opacity={0.18 + routeProgress.current * 0.82}
		style:transform={`translate3d(0, ${(1 - routeProgress.current) * 18}px, 0)`}
	>
		{@render children()}
	</main>

	<footer class="site-footer">
		<div>
			<strong>Samenbijeen</strong>
			<p>
				Persoonlijke begeleiding, coaching en ondersteuning voor jeugd, volwassenen en organisaties.
			</p>
		</div>
		<div class="footer-links">
			<a href={resolve('/contact')}>Contact</a>
			<a href={resolve('/zorg-ondersteuning')}>Zorg / ondersteuning</a>
			<a href={resolve('/begeleiding-coaching')}>Begeleiding / coaching</a>
		</div>
	</footer>
</div>
