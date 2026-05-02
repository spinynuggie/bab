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
	let menuOpen = $state(false);
	let headerProgress = $state(page.url.pathname === '/' ? 0 : 1);

	const routeProgress = new Tween(1, {
		duration: 560,
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
	const isHome = $derived(page.url.pathname === '/');
	const ease = (value: number) => value * value * (3 - 2 * value);
	const delayed = (value: number, start: number) =>
		Math.min(1, Math.max(0, (value - start) / (1 - start)));
	const headerTone = $derived(isHome ? headerProgress : 1);
	const headerSurface = $derived(isHome ? ease(delayed(headerProgress, 0.42)) : 1);
	const headerColor = $derived(
		`rgb(${Math.round(255 + (16 - 255) * headerTone)}, ${Math.round(
			255 + (45 - 255) * headerTone
		)}, ${Math.round(255 + (84 - 255) * headerTone)})`
	);
	const headerNavColor = $derived(
		`rgb(${Math.round(255 + (55 - 255) * headerTone)}, ${Math.round(
			255 + (81 - 255) * headerTone
		)}, ${Math.round(255 + (111 - 255) * headerTone)})`
	);
	const headerBackgroundOpacity = $derived(isHome ? headerSurface * 0.46 : 0.58);
	const headerLineOpacity = $derived(isHome ? headerSurface * 0.18 : 0.18);
	const headerBlur = $derived(`${Math.round((isHome ? headerSurface : 1) * 22)}px`);
	const headerGlassOpacity = $derived(isHome ? headerSurface : 1);
	const menuButtonBackground = $derived(
		isHome && headerProgress < 0.45 ? 'rgba(255, 255, 255, 0.14)' : '#ffffff'
	);

	onMount(() => {
		let frame = 0;

		const update = () => {
			frame = 0;
			headerProgress = page.url.pathname === '/' ? Math.min(1, window.scrollY / 220) : 1;
		};

		const schedule = () => {
			if (frame) return;
			frame = requestAnimationFrame(update);
		};

		update();
		window.addEventListener('scroll', schedule, { passive: true });
		window.addEventListener('resize', schedule);

		return () => {
			if (frame) cancelAnimationFrame(frame);
			window.removeEventListener('scroll', schedule);
			window.removeEventListener('resize', schedule);
		};
	});

	$effect(() => {
		const currentPath = page.url.pathname;

		if (currentPath === previousPath) {
			return;
		}

		previousPath = currentPath;
		menuOpen = false;
		headerProgress =
			currentPath === '/' && typeof window !== 'undefined' ? Math.min(1, window.scrollY / 220) : 1;

		if (prefersReducedMotion.current) {
			routeProgress.set(1, { duration: 0 });
			return;
		}

		routeProgress.set(0, { duration: 0 });
		routeProgress.set(1, { duration: 620, easing: cubicOut });
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&display=swap"
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
	class:home-shell={isHome}
	style:--header-color={headerColor}
	style:--header-nav-color={headerNavColor}
	style:--header-bg-opacity={headerBackgroundOpacity}
	style:--header-line-opacity={headerLineOpacity}
	style:--header-blur={headerBlur}
	style:--header-glass-opacity={headerGlassOpacity}
	style:--menu-button-bg={menuButtonBackground}
>
	<header class="site-header">
		<a class="brand" href={resolve('/')} aria-label="Samenbijeen home">
			<strong>Samenbijeen</strong>
		</a>

		<button
			class="menu-toggle"
			type="button"
			aria-label="Navigatie openen"
			aria-expanded={menuOpen}
			aria-controls="site-navigation"
			onclick={() => (menuOpen = !menuOpen)}
		>
			<span></span>
			<span></span>
		</button>

		<nav id="site-navigation" class:open={menuOpen} aria-label="Hoofdnavigatie">
			{#each navItems as item (item.href)}
				<a
					aria-current={isActive(item.href) ? 'page' : undefined}
					href={resolve(item.href)}
					onclick={() => (menuOpen = false)}
				>
					{item.label}
				</a>
			{/each}
		</nav>
	</header>

	<main
		style:opacity={0.18 + routeProgress.current * 0.82}
		style:transform={`translate3d(0, ${(1 - routeProgress.current) * 16}px, 0)`}
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
