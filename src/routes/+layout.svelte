<script lang="ts">
	import { resolve } from '$app/paths';
	import { page } from '$app/state';
	import { cubicOut } from 'svelte/easing';
	import { prefersReducedMotion, Tween } from 'svelte/motion';
	import { onMount, tick } from 'svelte';
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
	let previousPath = $state(page.url.pathname);
	let menuOpen = $state(false);
	let headerProgress = $state(page.url.pathname === '/' ? 0 : 1);
	let refreshReveals = () => {};

	const routeProgress = new Tween(1, {
		duration: 760,
		easing: cubicOut
	});

	const navItems = [
		{ href: '/', label: 'Home' },
		{ href: '/over-ons', label: 'Over ons' },
		{ href: '/begeleiding-coaching', label: 'Begeleiding' },
		{ href: '/samenwerkingen', label: 'Samenwerkingen' },
		{ href: '/contact', label: 'Contact' }
	] as const;

	const hrefParts = (href: string) => {
		const [path, hash] = href.split('#');
		return { path, hash: hash ? `#${hash}` : '' };
	};
	const isActive = (href: string) => {
		const { path, hash } = hrefParts(href);

		if (href === '/') return page.url.pathname === '/';
		if (hash) return page.url.pathname === path && page.url.hash === hash;
		return page.url.pathname === path && !page.url.hash;
	};
	const isHome = $derived(page.url.pathname === '/');
	const ease = (value: number) => value * value * (3 - 2 * value);
	const delayed = (value: number, start: number) =>
		Math.min(1, Math.max(0, (value - start) / (1 - start)));
	const headerTone = $derived(isHome ? headerProgress : 1);
	const headerSurface = $derived(isHome ? ease(delayed(headerProgress, 0.42)) : 1);
	const headerColor = $derived(
		`rgb(${Math.round(255 + (20 - 255) * headerTone)}, ${Math.round(
			255 + (35 - 255) * headerTone
		)}, ${Math.round(255 + (59 - 255) * headerTone)})`
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
		let revealObserver: IntersectionObserver | undefined;
		const revealSelector = [
			'.reveal',
			'.page-hero',
			'.section',
			'.contact-layout',
			'.site-footer',
			'.reveal-children',
			'.service-card'
		].join(',');

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

		if (prefersReducedMotion.current) {
			document.documentElement.classList.add('reveal-disabled');
			refreshReveals = () => {};
		} else {
			document.documentElement.classList.add('reveal-enabled');
			revealObserver = new IntersectionObserver(
				(entries) => {
					for (const entry of entries) {
						if (!entry.isIntersecting) continue;
						entry.target.classList.add('is-visible');
						revealObserver?.unobserve(entry.target);
					}
				},
				{ rootMargin: '0px 0px -12% 0px', threshold: 0.16 }
			);

			refreshReveals = () => {
				void tick().then(() => {
					document.querySelectorAll<HTMLElement>(revealSelector).forEach((element) => {
						if (element.classList.contains('is-visible')) return;
						revealObserver?.observe(element);
					});
				});
			};

			refreshReveals();
		}

		return () => {
			if (frame) cancelAnimationFrame(frame);
			window.removeEventListener('scroll', schedule);
			window.removeEventListener('resize', schedule);
			revealObserver?.disconnect();
			document.documentElement.classList.remove('reveal-enabled', 'reveal-disabled');
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
		routeProgress.set(1, { duration: 820, easing: cubicOut });
		refreshReveals();
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=DM+Serif+Display:ital@0;1&display=swap"
		rel="stylesheet"
	/>
	<title>Samenbijeen | Begeleiding op maat</title>
	<meta
		name="description"
		content="Samenbijeen biedt betrokken en persoonlijke begeleiding op maat."
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
			<img src="/images/samenbijeen-logo.png" alt="Samenbijeen begeleiding op maat" />
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
			<img
				class="footer-logo"
				src="/images/samenbijeen-logo.png"
				alt="Samenbijeen begeleiding op maat"
			/>
			<p>Betrokken en persoonlijke begeleiding op maat.</p>
		</div>
		<div class="footer-links">
			<a href={resolve('/over-ons')}>Over ons</a>
			<a href={resolve('/begeleiding-coaching')}>Begeleiding</a>
			<a href={resolve('/samenwerkingen')}>Samenwerkingen</a>
			<a href={resolve('/contact')}>Contact</a>
			<a href={resolve('/solliciteren')}>Solliciteren</a>
		</div>
		<div class="footer-contact">
			<span>Genemuidenstraat 208, unit 925</span>
			<span>2545 NZ Den Haag</span>
			<a href="mailto:info@samenbijeen.nl">info@samenbijeen.nl</a>
			<a href="tel:+31622229975">06 2222 9975</a>
			<span>Instagram: Samenbijeen</span>
		</div>
	</footer>
</div>
