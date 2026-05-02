<script lang="ts">
	import WidePhoto from '$lib/WidePhoto.svelte';

	const support = [
		'Ambulante begeleiding en begeleiding aan huis',
		'Persoonlijke verzorging en medicatieondersteuning',
		'Huishoudelijke hulp en praktische ondersteuning',
		'Koken, maaltijden bereiden en gezonde routines',
		'Activiteiten, dagbesteding en sociale deelname',
		'Veiligheid, stabiliteit en ondersteuning van het netwerk'
	];
</script>

<svelte:head>
	<title>Zorg / ondersteuning | Samenbijeen</title>
</svelte:head>

<section class="page-hero">
	<h1>Ondersteuning op alle vlakken van het dagelijks leven.</h1>
	<p>
		Iedereen verdient een volwaardig leven: gezien worden, gehoord worden, zelfstandig kunnen
		functioneren en onderdeel zijn van de maatschappij.
	</p>
</section>

<WidePhoto src="/images/page-support.svg" alt="Abstracte visual over zorg en ondersteuning" />

<section class="section">
	<div class="section-heading">
		<h2>Breed, praktisch en afgestemd op de situatie.</h2>
	</div>
	<div class="support-grid">
		{#each support as item, index (item)}
			<div class="reveal" style={`--delay: ${index * 70}ms`}>{item}</div>
		{/each}
	</div>
</section>

<section class="section split">
	<div>
		<h2>Mensgericht en methodisch.</h2>
	</div>
	<div class="copy-stack reveal delay-1">
		<p>
			Een betekenisvolle relatie staat centraal. Wij werken vanuit vertrouwen, gelijkwaardigheid en
			wederzijds respect.
		</p>
		<p>
			Met een methodische aanpak houden cliënt en begeleider zicht op doelen, voortgang en wat er
			nodig is om blijvend verschil te maken.
		</p>
	</div>
</section>
