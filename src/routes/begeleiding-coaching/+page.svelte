<script lang="ts">
	import ResponsiveImage from '$lib/ResponsiveImage.svelte';
	import RevealText from '$lib/RevealText.svelte';

	const tracks = [
		{
			title: 'Jongeren',
			text: 'Begeleiding wanneer school, thuis of het dagelijks leven vastloopt. Samen werken we aan rust, overzicht en zelfvertrouwen.'
		},
		{
			title: 'Volwassenen',
			text: 'Een veilige en vertrouwde plek waar jouw verhaal gehoord wordt. We werken stap voor stap aan kracht, rust en regie.'
		},
		{
			title: 'Kind & gezin',
			text: 'Ondersteuning voor gezinnen die meer balans, duidelijkheid en stabiliteit nodig hebben in de thuissituatie.'
		},
		{
			title: 'Ambulante begeleiding',
			text: 'Begeleiding aan huis bij administratie, financiën, huishouden en structuur in het dagelijks leven.'
		}
	];

	const support = [
		'Administratie en financiën',
		'Huishoudelijke ondersteuning',
		'Structuur in het dagelijks leven',
		'Passend dagritme opbouwen',
		'Werk, vrijwilligerswerk of dagbesteding',
		'Regie over het eigen leven terugpakken'
	];
</script>

<svelte:head>
	<title>Begeleiding / coaching | Samenbijeen</title>
</svelte:head>

<section class="page-hero">
	<h1>Begeleiding die aansluit bij jouw situatie.</h1>
	<p>
		Iedere jongere is uniek. Daarom bieden wij begeleiding die aansluit bij jouw persoonlijke
		situatie. Wij werken samen met jou, stap voor stap, aan oplossingen die bij jou passen.
	</p>
</section>

<section class="section split guidance-section">
	<div class="copy-stack reveal">
		<RevealText text="Overzicht, rust en zelfvertrouwen" />
		<p>
			Onze begeleiding is gericht op het creëren van overzicht, rust en zelfvertrouwen. Samen kijken
			we naar wat jij nodig hebt en werken we stap voor stap aan oplossingen die bij jou passen.
		</p>
		<div class="guidance-card-list">
			{#each tracks as track, index (track.title)}
				<article class="service-card compact reveal" style={`--delay: ${index * 90}ms`}>
					<h3>{track.title}</h3>
					<p>{track.text}</p>
				</article>
			{/each}
		</div>
	</div>
	<div class="reveal delay-1">
		<ResponsiveImage
			class="content-photo"
			src="/images/content/richting-900.webp"
			srcset="/images/content/richting-900.webp 900w, /images/content/richting-1200.webp 1200w"
			sizes="(max-width: 900px) 100vw, 46vw"
			alt="Wegwijzers als symbool voor richting vinden"
		/>
	</div>
</section>

<section class="section quote-section reveal delay-1">
	<blockquote>“Bij Samenbijeen staan we naast je.”</blockquote>
	<p>
		We werken aan een passend dagritme, praktische vaardigheden en deelname aan school, werk,
		vrijwilligerswerk of dagbesteding. Ook ondersteunen we bij het terugpakken van regie over het
		eigen leven.
	</p>
</section>

<section class="section split guidance-section">
	<div class="copy-stack reveal">
		<RevealText text="Ambulante begeleiding" />
		<p>
			Samenbijeen biedt ambulante begeleiding aan huis voor jongeren, volwassenen en gezinnen die
			vastlopen in het dagelijks leven. Samen werken we aan meer rust, structuur en stabiliteit,
			zodat je zo zelfstandig mogelijk kunt blijven wonen.
		</p>
		<p>
			Wij ondersteunen bij onder andere administratie, financiën, het huishouden en het aanbrengen
			van structuur in het dagelijks leven.
		</p>
		<div class="glass-pills inline-pills">
			{#each support as item (item)}
				<span>{item}</span>
			{/each}
		</div>
	</div>
	<div class="reveal delay-1">
		<ResponsiveImage
			class="content-photo"
			src="/images/content/road-900.webp"
			srcset="/images/content/road-900.webp 900w, /images/content/road-1400.webp 1400w"
			sizes="(max-width: 900px) 100vw, 46vw"
			alt="Een open weg als symbool voor stap voor stap vooruitgaan"
		/>
	</div>
</section>

<section class="section split coaching-section">
	<div class="copy-stack reveal">
		<RevealText text="Coaching traject Samenbijeen" />
		<p>
			Wij bieden coaching trajecten aan in binnen- en buitenland. Tijdelijk afstand nemen van de
			dagelijkse omgeving kan helpen om patronen te doorbreken en ruimte te creëren voor rust,
			overzicht en reflectie.
		</p>
		<p>
			De trajecten kunnen variëren van een paar dagen of weekend tot langere trajecten. Het doel is
			dat je sterker, bewuster en met meer vertrouwen terugkeert naar je dagelijks leven.
		</p>
	</div>
	<div class="reveal delay-1">
		<ResponsiveImage
			class="content-photo"
			src="/images/content/coaching-journey-900.webp"
			srcset="/images/content/coaching-journey-900.webp 900w, /images/content/coaching-journey-1400.webp 1400w"
			sizes="(max-width: 900px) 100vw, 46vw"
			alt="Rustige reisomgeving als symbool voor afstand nemen en reflectie"
		/>
	</div>
</section>
