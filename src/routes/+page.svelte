<script lang="ts">
	import { resolve } from '$app/paths';
	import RevealText from '$lib/RevealText.svelte';
	import { onMount } from 'svelte';

	let heroElement: HTMLElement;
	let heroProgress = $state(0);

	const clamp = (value: number) => Math.min(1, Math.max(0, value));
	const heroVisualOpacity = $derived(1 - heroProgress * 0.78);
	const heroVisualScale = $derived(1 + heroProgress * 0.055);
	const heroContentY = $derived(heroProgress * -22);
	const heroTextColor = $derived(
		`rgb(${Math.round(255 + (20 - 255) * heroProgress)}, ${Math.round(
			255 + (35 - 255) * heroProgress
		)}, ${Math.round(255 + (59 - 255) * heroProgress)})`
	);
	const heroMutedColor = $derived(
		`rgb(${Math.round(235 + (92 - 235) * heroProgress)}, ${Math.round(
			244 + (109 - 244) * heroProgress
		)}, ${Math.round(255 + (134 - 255) * heroProgress)})`
	);
	const heroButtonText = $derived(heroProgress < 0.5 ? '#102d54' : '#ffffff');

	onMount(() => {
		let frame = 0;
		let heroTop = 0;
		let heroScrollable = 1;

		const measure = () => {
			if (!heroElement) return;
			heroTop = heroElement.offsetTop;
			heroScrollable = Math.max(1, heroElement.offsetHeight - window.innerHeight);
		};

		const update = () => {
			frame = 0;
			heroProgress = clamp((window.scrollY - heroTop) / heroScrollable);
		};

		const schedule = () => {
			if (frame) return;
			frame = requestAnimationFrame(update);
		};

		const resize = () => {
			measure();
			schedule();
		};

		measure();
		schedule();
		window.addEventListener('scroll', schedule, { passive: true });
		window.addEventListener('resize', resize);

		return () => {
			if (frame) cancelAnimationFrame(frame);
			window.removeEventListener('scroll', schedule);
			window.removeEventListener('resize', resize);
		};
	});

	const highlights = [
		'Persoonlijke begeleiding op maat',
		'Oprechte betrokkenheid en vertrouwen',
		'Brede expertise voor jongeren en volwassenen',
		'Stap voor stap werken aan zelfstandigheid'
	];

	const services = [
		{
			title: 'Ik zoek hulp',
			text: 'Samen kijken we naar wat jij nodig hebt en werken we stap voor stap aan rust, structuur en zelfvertrouwen.',
			href: '/ik-zoek-hulp'
		},
		{
			title: 'Begeleiding / coaching',
			text: 'Begeleiding bij rust, structuur, zelfvertrouwen en richting.',
			href: '/begeleiding-coaching'
		},
		{
			title: 'Zorg / ondersteuning',
			text: 'Praktische ondersteuning in het dagelijks leven en bij zorgvragen.',
			href: '/zorg-ondersteuning'
		}
	] as const;

	const moments = [
		{
			src: '/images/story-care.svg',
			alt: 'Abstracte illustratie over zorg en rust',
			title: 'Persoonlijke begeleiding op maat',
			text: 'Iedere mens is uniek. Wij stemmen onze begeleiding volledig af op jouw persoonlijke situatie, wensen en mogelijkheden.'
		},
		{
			src: '/images/story-coaching.svg',
			alt: 'Abstracte illustratie over coaching en gesprek',
			title: 'Oprechte betrokkenheid',
			text: 'Wij staan naast jou en bouwen aan een vertrouwensband waarin jij je gehoord en begrepen voelt.'
		},
		{
			src: '/images/story-community.svg',
			alt: 'Abstracte illustratie over samen in de wijk',
			title: 'Werken aan zelfstandigheid',
			text: 'Samen werken we stap voor stap aan meer zelfredzaamheid, stabiliteit en grip op het dagelijks leven.'
		}
	] as const;
</script>

<svelte:head>
	<title>Samenbijeen | Home</title>
</svelte:head>

<section
	class="hero"
	bind:this={heroElement}
	style:--hero-visual-opacity={heroVisualOpacity}
	style:--hero-visual-scale={heroVisualScale}
	style:--hero-content-y={`${heroContentY}px`}
	style:--hero-text={heroTextColor}
	style:--hero-muted={heroMutedColor}
	style:--hero-button-text={heroButtonText}
>
	<div class="hero-visual" aria-hidden="true"></div>

	<div class="hero-copy reveal">
		<h1>Samenbijeen geeft richting.</h1>
		<p class="lede">
			Wij begeleiden volwassenen en jongeren die extra ondersteuning nodig hebben om weer grip te
			krijgen op hun leven. Samen kijken we naar wat nodig is en werken we stap voor stap aan rust,
			structuur en zelfvertrouwen.
		</p>
		<div class="hero-actions">
			<a class="button primary" href={resolve('/ik-zoek-hulp')}>Ik zoek hulp</a>
			<a class="button secondary" href={resolve('/solliciteren')}>Kom werken bij ons</a>
		</div>
	</div>
</section>

<section class="image-story centered reveal delay-1">
	<div class="section-heading">
		<RevealText text="Overzicht, rust en vertrouwen." />
		<p>
			Bij Samenbijeen geloven we dat iedereen recht heeft op een volwaardig en betekenisvol leven.
			Wij bieden persoonlijke begeleiding die aansluit bij de individuele situatie.
		</p>
	</div>
	<div class="image-row reveal-children">
		{#each moments as moment, index (moment.src)}
			<figure class="image-tile" style={`--card-delay: ${index * 160}ms`}>
				<img src={moment.src} alt={moment.alt} loading="lazy" decoding="async" />
				<figcaption>
					<strong>{moment.title}</strong>
					<span>{moment.text}</span>
				</figcaption>
			</figure>
		{/each}
	</div>
</section>

<section class="section centered-support">
	<div class="section-heading reveal">
		<RevealText text="Onze begeleiding" />
		<p>
			Onze missie is om jongeren en volwassenen te begeleiden op weg naar stabiliteit en
			zelfredzaamheid. De begeleiding is gebaseerd op betrokkenheid, aandacht en maatwerk.
		</p>
	</div>
	<ul class="glass-pills reveal">
		{#each highlights as highlight (highlight)}
			<li>{highlight}</li>
		{/each}
	</ul>
</section>

<section class="section split">
	<div class="reveal">
		<RevealText text="Missie en visie" />
	</div>
	<div class="copy-stack reveal delay-1">
		<p>
			Wij geloven dat niemand er alleen voor hoeft te staan. Samen kijken we naar wat iemand nodig
			heeft om weer grip, vertrouwen en richting te vinden.
		</p>
		<p>
			Echte verandering ontstaat wanneer mensen zich gezien, gehoord en ondersteund voelen. Daarom
			werken wij vanuit verbinding, betrokkenheid en samenwerking.
		</p>
	</div>
</section>

<section class="section">
	<div class="section-heading reveal">
		<RevealText text="Plan een intake in" />
	</div>

	<div class="service-grid">
		{#each services as service, index (service.href)}
			<a
				class="service-card reveal"
				style={`--delay: ${index * 90}ms`}
				href={resolve(service.href)}
			>
				<span>0{index + 1}</span>
				<h3>{service.title}</h3>
				<p>{service.text}</p>
				<em>Bekijk pagina</em>
			</a>
		{/each}
	</div>
</section>

<section class="cta-band reveal">
	<div>
		<h2>Samen maken we het verschil.</h2>
	</div>
	<div class="hero-actions">
		<a class="button primary" href={resolve('/contact')}>Neem contact op</a>
		<a class="button secondary" href={resolve('/solliciteren')}>Solliciteren</a>
	</div>
</section>
