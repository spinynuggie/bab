<svelte:head>
	<title>Contact | Samenbijeen</title>
</svelte:head>

<section class="page-hero">
	<h1>Professionals die het verschil maken.</h1>
	<p>
		Zoek je hulp, wil je overleggen over een naaste, of heb je als organisatie flexibele
		zorgprofessionals nodig? Neem contact op met Samenbijeen.
	</p>
</section>

<section class="contact-layout">
	<form class="contact-form reveal delay-1">
		<label>
			Naam
			<input name="name" type="text" autocomplete="name" />
		</label>
		<label>
			E-mail
			<input name="email" type="email" autocomplete="email" />
		</label>
		<label>
			Waar kunnen we mee helpen?
			<select name="topic">
				<option>Ik zoek hulp</option>
				<option>Ik zoek een zorgprofessional</option>
				<option>Algemene vraag</option>
			</select>
		</label>
		<label>
			Bericht
			<textarea name="message" rows="5"></textarea>
		</label>
		<button class="button primary" type="submit">Verstuur bericht</button>
	</form>

	<aside class="contact-card reveal delay-2">
		<img
			class="contact-photo"
			src="/images/contact-team.svg"
			alt="Abstracte visual over zorgteam overleg"
			loading="lazy"
			decoding="async"
		/>
		<h2>Voor iedere zorgvraag de juiste match.</h2>
		<p>
			Samenbijeen verbindt zorginstellingen met betrokken zorgverleners op flexibele basis,
			gedetacheerd of in vaste dienst.
		</p>
		<div class="contact-lines">
			<span>info@samenbijeen.nl</span>
			<span>Nederland</span>
		</div>
	</aside>
</section>
