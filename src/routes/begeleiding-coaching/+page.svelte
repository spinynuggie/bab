<script lang="ts">
	import ResponsiveImage from '$lib/ResponsiveImage.svelte';
	import RevealText from '$lib/RevealText.svelte';

	const anchors = [
		{ label: 'Coaching traject', id: 'coaching-traject' },
		{ label: 'Ambulante begeleiding', id: 'ambulante-begeleiding' },
		{ label: 'Jongeren', id: 'jongeren' },
		{ label: 'Volwassenen', id: 'volwassenen' },
		{ label: 'Kind & gezin', id: 'kind-gezin' }
	] as const;
</script>

<svelte:head>
	<title>Begeleiding / coaching | Samenbijeen</title>
</svelte:head>

<section class="page-hero compact">
	<h1>Begeleiding</h1>
	<p>
		De begeleiding is persoonlijk en intensief. We staan dicht naast de persoon en kijken samen naar
		wat nodig is om verder te komen. Het doel is om meer zelfvertrouwen, richting en balans te
		ontwikkelen.
	</p>
</section>

<nav class="section-tabs reveal" aria-label="Onderdelen begeleiding">
	{#each anchors as anchor (anchor.id)}
		<a href={`#${anchor.id}`}>{anchor.label}</a>
	{/each}
</nav>

<ResponsiveImage
	class="wide-content-photo"
	src="/images/content/coaching-journey-900.webp"
	srcset="/images/content/coaching-journey-900.webp 900w, /images/content/coaching-journey-1400.webp 1400w"
	sizes="(max-width: 900px) 100vw, 1180px"
	alt="Rustige reisomgeving als symbool voor afstand nemen en reflectie"
/>

<section id="coaching-traject" class="section split guidance-feature">
	<div class="section-kicker reveal delay-1">
		<span>01</span>
		<RevealText text="Coaching Traject Samenbijeen" />
	</div>
	<div class="copy-stack guidance-copy reveal delay-1">
		<p>
			Wij bieden coaching trajecten aan in binnen- en buitenland. Door tijdelijk afstand te nemen
			van je dagelijkse omgeving ontstaat er ruimte voor rust, overzicht en nieuwe inzichten. Dit
			helpt je om patronen te doorbreken en weer richting te vinden.
		</p>
		<p>
			De begeleiding is persoonlijk en gericht op het versterken van je zelfvertrouwen, het vinden
			van richting en het herstellen van balans.
		</p>
		<p>
			De trajecten kunnen variëren van een paar dagen of een weekend tot langere trajecten van
			enkele weken of maanden. Het doel is dat je sterker, bewuster en met meer vertrouwen
			terugkeert naar je dagelijks leven.
		</p>
	</div>
</section>

<section id="ambulante-begeleiding" class="section split guidance-feature reversed">
	<div class="section-kicker reveal">
		<span>02</span>
		<RevealText text="Ambulante begeleiding" />
	</div>
	<div class="copy-stack guidance-copy reveal delay-1">
		<p>
			Samenbijeen biedt ambulante begeleiding aan huis voor jongeren, volwassenen en gezinnen die
			vastlopen in het dagelijks leven. Samen werken we aan meer rust, structuur en stabiliteit,
			zodat je zo zelfstandig mogelijk kunt blijven wonen.
		</p>
		<p>
			Deze ondersteuning is bedoeld voor jongeren, volwassenen en gezinnen die op meerdere
			leefgebieden vastlopen. Heb je te maken met een beperking, een verslaving, een beperkt sociaal
			netwerk of met gebeurtenissen en ervaringen die invloed hebben op je leven?
		</p>
		<p>
			Samen kijken we naar jouw situatie en werken we stap voor stap aan herstel, rust en
			stabiliteit. Wij ondersteunen bij onder andere administratie, financiën, het huishouden en het
			aanbrengen van structuur in het dagelijks leven.
		</p>
	</div>
</section>

<section id="jongeren" class="section split guidance-feature">
	<div class="section-kicker reveal">
		<span>03</span>
		<RevealText text="Individuele Begeleiding Jongeren" />
	</div>
	<div class="copy-stack guidance-copy reveal delay-1">
		<p>
			Je loopt vast op school of in het dagelijks leven, of je merkt dat het lastig is om overzicht
			te houden, bijvoorbeeld in je financiën of planning. Dit kan bijvoorbeeld ontstaan door
			ingrijpende gebeurtenissen of eerdere ervaringen.
		</p>
		<p>
			Iedere jongere is uniek. Daarom bieden wij begeleiding die aansluit bij jouw persoonlijke
			situatie. Wij werken samen met jou, stap voor stap, aan oplossingen die bij jou passen. Jij
			staat centraal in het traject.
		</p>
		<p>
			Onze begeleiding is gericht op het creëren van rust, overzicht en zelfvertrouwen. Samen werken
			we eraan dat je weer overzicht krijgt, sterker in je schoenen staat en stappen kunt zetten
			naar een betere toekomst.
		</p>
	</div>
</section>

<section id="volwassenen" class="section split guidance-feature reversed">
	<div class="section-kicker reveal">
		<span>04</span>
		<RevealText text="Individuele Begeleiding Volwassenen" />
	</div>
	<div class="copy-stack guidance-copy reveal delay-1">
		<p>
			Soms brengt het leven uitdagingen met zich mee die zwaar kunnen voelen. Je draagt bijvoorbeeld
			ervaringen uit het verleden met je mee of merkt dat je vastloopt in bepaalde situaties.
		</p>
		<p>
			Bij Samenbijeen bieden we een veilige en vertrouwde plek waar jouw verhaal gehoord wordt.
			Samen kijken we naar wat jij nodig hebt en werken we stap voor stap aan meer rust, kracht en
			zelfvertrouwen.
		</p>
		<p>
			Onze begeleiding sluit aan bij jouw persoonlijke situatie. Bij Samenbijeen staan we naast je.
		</p>
	</div>
</section>

<section id="kind-gezin" class="section split guidance-feature">
	<div class="section-kicker reveal">
		<span>05</span>
		<RevealText text="Kind & Gezin" />
	</div>
	<div class="copy-stack guidance-copy reveal delay-1">
		<p>
			Een gezin waarin rust en structuur centraal staan, helpt kinderen en ouders om zich goed te
			ontwikkelen. Wij bieden begeleiding aan gezinnen waarbij we samen kijken naar wat er nodig is
			om meer balans, overzicht en stabiliteit te creëren.
		</p>
		<p>
			Loop je als ouder vast of zit je in een moeilijke situatie door een gebeurtenis, een beperking
			of andere omstandigheden? Bij Samenbijeen staan we naast je.
		</p>
		<p>
			Samen kijken we naar wat er speelt en wat jouw gezin nodig heeft. We werken aan praktische
			oplossingen die helpen in het dagelijks leven. Zo bouwen we stap voor stap aan meer balans,
			duidelijkheid en een stabiele thuissituatie voor het hele gezin.
		</p>
	</div>
</section>
