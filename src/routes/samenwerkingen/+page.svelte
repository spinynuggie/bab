<script lang="ts">
	import ResponsiveImage from '$lib/ResponsiveImage.svelte';
	import RevealText from '$lib/RevealText.svelte';
</script>

<svelte:head>
	<title>Samenwerkingen | Samenbijeen</title>
</svelte:head>

<section class="page-hero compact centered-page-hero">
	<h1>Samenwerkingen</h1>
	<p>
		Wij ondersteunen zorgorganisaties bij het creëren van een veilige en professioneel ingerichte
		zorglocatie van A tot Z.
	</p>
	<p>
		Denk hierbij aan structuur, aansturing van zorgteams, veiligheidsbeleid, werkprocessen,
		protocollen, ervaren begeleiders en begeleidingsmethodieken. Daarnaast denken wij mee over
		kwaliteitseisen, verantwoordelijkheden en een duurzame inrichting van de zorgverlening.
	</p>
	<p>
		Met onze praktijkervaring binnen de welzijnssector bieden wij een stevige basis waarop een
		zorglocatie professioneel en toekomstbestendig kan functioneren.
	</p>
</section>

<ResponsiveImage
	class="wide-content-photo"
	src="/images/content/samen-sterk-900.webp"
	srcset="/images/content/samen-sterk-900.webp 900w, /images/content/samen-sterk-1400.webp 1400w"
	sizes="(max-width: 900px) 100vw, 1180px"
	alt="Mensen die elkaar helpen omhoog te klimmen"
/>

<section class="section split">
	<div class="reveal">
		<RevealText text="Gekwalificeerde begeleiders" />
	</div>
	<div class="copy-stack reveal delay-1">
		<p>
			Wij ondersteunen zorgorganisaties, thuiszorg en gemeenten bij het vinden van gekwalificeerde
			begeleiders. Dit kan gaan om complexe situaties waarin begeleiding nodig is, of waarbij
			cliënten tijdelijk of structureel 24-uurs begeleiding of ondersteuning nodig hebben.
		</p>
		<p>
			Ons doel is het creëren van stabiliteit, zodat passende ondersteuning gewaarborgd blijft. Wij
			zorgen voor een zorgvuldige match.
		</p>
	</div>
</section>
