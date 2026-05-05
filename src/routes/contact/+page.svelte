<svelte:head>
	<title>Contact | Samenbijeen</title>
</svelte:head>

<section class="page-hero compact centered-page-hero">
	<h1>Contact</h1>
	<p>
		Welkom bij Samenbijeen. Wij bieden betrokken en persoonlijke begeleiding op maat. Heeft u
		vragen, behoefte aan advies of wilt u weten wat wij voor u of uw organisatie kunnen betekenen?
		Neem gerust contact met ons op.
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
				<option>Begeleiding</option>
				<option>Ik zoek gekwalificeerde begeleiders</option>
				<option>Ik wil solliciteren</option>
				<option>Algemene vraag</option>
			</select>
		</label>
		<label>
			Bericht
			<textarea name="message" rows="5"></textarea>
		</label>
		<button class="button primary" type="submit">Verstuur bericht</button>
	</form>

	<aside class="contact-card-real reveal delay-2">
		<img src="/images/samenbijeen-logo.png" alt="Samenbijeen begeleiding op maat" />
		<div class="contact-info">
			<strong>Contact</strong>
			<p>Neem gerust contact met ons op.</p>
			<div class="contact-lines">
				<span>info@samenbijeen.nl</span>
				<span>06 2222 9975</span>
				<span>Genemuidenstraat 208 unit 9, 2545 NZ Den Haag</span>
				<span>Instagram: Samenbijeen</span>
			</div>
		</div>
	</aside>
</section>
