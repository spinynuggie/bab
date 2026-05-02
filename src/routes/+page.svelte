<script lang="ts">
	import { resolve } from '$app/paths';
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
		'Begeleiding aan huis, op school, op werk of in de wijk',
		'Een vaste begeleider waar dat kan, korte lijnen waar dat nodig is',
		'Praktische ondersteuning voor cliënten, naasten en zorgorganisaties'
	];

	const services = [
		{
			title: 'Ik zoek hulp',
			text: 'Samen kijken we welke begeleiding past bij jouw situatie, tempo en doelen.',
			href: '/ik-zoek-hulp'
		},
		{
			title: 'Begeleiding / coaching',
			text: 'Doelgerichte begeleiding bij structuur, zelfvertrouwen, sociale vaardigheden en herstel.',
			href: '/begeleiding-coaching'
		},
		{
			title: 'Zorg / ondersteuning',
			text: 'Ondersteuning in het dagelijks leven, van ambulante begeleiding tot praktische zorg.',
			href: '/zorg-ondersteuning'
		}
	] as const;

	const moments = [
		{
			src: '/images/story-care.svg',
			alt: 'Abstracte illustratie over zorg en rust'
		},
		{
			src: '/images/story-coaching.svg',
			alt: 'Abstracte illustratie over coaching en gesprek'
		},
		{
			src: '/images/story-community.svg',
			alt: 'Abstracte illustratie over samen in de wijk'
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
		<h1>Rustige hulp voor mensen die weer grip willen krijgen.</h1>
		<p class="lede">
			Samenbijeen helpt bij vragen die thuis, op school, op werk of in het dagelijks leven te groot
			zijn geworden. We luisteren eerst, maken daarna pas een plan.
		</p>
		<div class="hero-actions">
			<a class="button primary" href={resolve('/ik-zoek-hulp')}>Ik zoek hulp</a>
			<a class="button secondary" href={resolve('/contact')}>Ik zoek een professional</a>
		</div>
	</div>
</section>

<section class="image-story reveal delay-1">
	<div>
		<h2>Niet iedereen heeft dezelfde soort hulp nodig.</h2>
		<p>
			De ene persoon heeft vooral structuur nodig. De ander zoekt rust in het gezin, ondersteuning
			bij zelfstandigheid of een professional die tijdelijk kan bijspringen.
		</p>
	</div>
	<div class="image-row reveal-children">
		{#each moments as moment (moment.src)}
			<img src={moment.src} alt={moment.alt} loading="lazy" decoding="async" />
		{/each}
	</div>
</section>

<section class="section split">
	<div class="reveal">
		<h2>Zorg die klein genoeg blijft om iemand echt te zien.</h2>
	</div>
	<div class="copy-stack reveal delay-1">
		<p>
			Wij helpen mensen vaardigheden ontwikkelen, zelfvertrouwen versterken en zelfstandigheid
			vergroten. Ons doel is dat iemand weer steviger kan deelnemen aan het dagelijks leven.
		</p>
		<ul class="check-list">
			{#each highlights as highlight (highlight)}
				<li>{highlight}</li>
			{/each}
		</ul>
	</div>
</section>

<section class="section">
	<div class="section-heading reveal">
		<h2>Waar kom je voor?</h2>
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
		<h2>Een kort gesprek is vaak genoeg om richting te vinden.</h2>
	</div>
	<a class="button primary" href={resolve('/contact')}>Neem contact op</a>
</section>
