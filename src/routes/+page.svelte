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
	const buttonsSwapped = $derived(heroProgress > 0.56);

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

	const services = [
		{
			title: 'Begeleiding',
			text: 'Persoonlijke en doelgerichte begeleiding voor jongeren, volwassenen en gezinnen.',
			href: '/begeleiding-coaching'
		},
		{
			title: 'Samenwerkingen',
			text: 'Ondersteuning voor zorgorganisaties, thuiszorg, gemeenten en samenwerkingspartners.',
			href: '/samenwerkingen'
		},
		{
			title: 'Contact',
			text: 'Heeft u vragen, behoefte aan advies of wilt u weten wat wij voor u kunnen betekenen?',
			href: '/contact'
		}
	] as const;

	const values = [
		{
			title: 'Persoonlijke begeleiding op maat',
			text: 'Iedere mens is uniek. Wij stemmen onze begeleiding volledig af op jouw persoonlijke situatie, wensen en mogelijkheden.'
		},
		{
			title: 'Oprechte betrokkenheid',
			text: 'Wij staan naast jou en bouwen aan een vertrouwensband waarin jij je gehoord en begrepen voelt.'
		},
		{
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
>
	<div class="hero-visual" aria-hidden="true"></div>

	<div class="hero-copy reveal">
		<h1>Samenbijeen geeft richting.</h1>
		<p class="lede">
			Samenbijeen begeleidt volwassenen en jongeren die extra ondersteuning nodig hebben om weer
			grip te krijgen op hun leven. Samen kijken we naar wat ze nodig hebben en werken we stap voor
			stap aan rust, structuur en zelfvertrouwen, zodat zij weer vooruit kunnen.
		</p>
		<div class="hero-actions">
			<a
				class="button hero-primary"
				class:is-soft={buttonsSwapped}
				href={resolve('/begeleiding-coaching')}>Bekijk begeleiding</a
			>
			<a
				class="button hero-secondary"
				class:is-filled={buttonsSwapped}
				href={resolve('/solliciteren')}>Kom werken bij ons</a
			>
		</div>
	</div>
</section>

<section class="section centered-support">
	<div class="section-heading">
		<RevealText text="Overzicht, rust en vertrouwen." />
		<p>
			Bij Samenbijeen geloven we dat iedereen recht heeft op een volwaardig en betekenisvol leven.
			Wij begeleiden zowel volwassenen als jongeren.
		</p>
	</div>
	<div class="copy-stack home-copy reveal delay-1">
		<p>
			Wij bieden persoonlijke begeleiding die aansluit bij de individuele situatie. Hierbij kan
			gedacht worden aan ondersteuning bij administratie, huishoudelijke hulp en begeleiding gericht
			op het (her)vinden van regie over het eigen leven.
		</p>
		<p>
			Onze missie is om hen te begeleiden op weg naar stabiliteit en zelfredzaamheid. De begeleiding
			is gebaseerd op betrokkenheid, aandacht en maatwerk. Samenbijeen zet zich ervoor in dat zij
			weer kunnen deelnemen aan de maatschappij en vooruitgang kunnen boeken in het dagelijks leven.
			Bij Samenbijeen staan we naast hen.
		</p>
	</div>
</section>

<section class="section split">
	<div class="reveal">
		<RevealText text="Onze begeleiding" />
	</div>
	<div class="copy-stack reveal delay-1">
		<h3>Persoonlijke begeleiding op maat</h3>
		<p>
			Iedere mens is uniek. Wij stemmen onze begeleiding volledig af op jouw persoonlijke situatie,
			wensen en mogelijkheden.
		</p>
		<a class="button secondary" href={resolve('/begeleiding-coaching')}>Bekijk begeleiding</a>
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

<section class="section centered-support">
	<div class="section-heading reveal">
		<RevealText text="Waar wij voor staan" />
	</div>
	<div class="service-grid">
		{#each values as value, index (value.title)}
			<article class="service-card reveal" style={`--delay: ${index * 100}ms`}>
				<h3>{value.title}</h3>
				<p>{value.text}</p>
			</article>
		{/each}
	</div>
</section>

<section class="cta-band reveal">
	<div>
		<h2>Kom je werken bij Samenbijeen?</h2>
		<p>
			Samen maken we het verschil. Met langdurige trajecten en projecten zetten wij ons in voor
			begeleiding en ondersteuning van hoge kwaliteit. Wij werken vanuit betrokkenheid, aandacht en
			professionaliteit. Door maatwerk te bieden, bouwen we samen elke dag verder aan sterke en
			betekenisvolle begeleiding.
		</p>
	</div>
	<div class="hero-actions">
		<a class="button primary" href={resolve('/contact')}>Neem contact op</a>
		<a class="button secondary" href={resolve('/solliciteren')}>Solliciteren</a>
	</div>
</section>
