<script>
	const images = {
		rock: {
			src: 'images/rock.png',
			alt: 'rock'
		},
		paper: {
			src: 'images/paper.png',
			alt: 'paper'
		},
		scissors: {
			src: 'images/scissors.png',
			alt: 'scissors'
		}
	}

	let playerImage = images.rock
	let enemyImage = images.rock

	const randomNumber = (min, max) => {
		return Math.floor(Math.random() * (max - min + 1)) + min
	}

	//Scores
	let playerScore = 0
	let enemyScore = 0

	const updatePlayer = (button) => {
		if (button === 'rock') playerImage = images.rock
		if (button === 'paper') playerImage = images.paper
		if (button === 'scissors') playerImage = images.scissors
	}

	const updateEnemy = (num) => {
		if (num === 0) enemyImage = images.rock
		if (num === 1) enemyImage = images.paper
		if (num === 2) enemyImage = images.scissors
	}

	const updateScore = (player, enemy) => {
		if (player === 'rock' && enemy === 'scissors') playerScore++
		if (player === 'paper' && enemy === 'rock') playerScore++
		if (player === 'scissors' && enemy === 'paper') playerScore++

		if (enemy === 'rock' && player === 'scissors') enemyScore++
		if (enemy === 'paper' && player === 'rock') enemyScore++
		if (enemy === 'scissors' && player === 'paper') enemyScore++
	}

	const buttonClick = (button) => {
		updatePlayer(button)
		updateEnemy(randomNumber(0, 2))
		updateScore(playerImage.alt, enemyImage.alt)
	}

</script>

<main>
	<h2>Score: {playerScore} - {enemyScore}</h2>
	<div id='game'>

		<div>
			<h1>Player</h1>
			<img src='{playerImage.src}' alt='{playerImage.alt}' width='64px' height='64px'>
		</div>

		<div>
			<h1>Enemy</h1>
			<img src='{enemyImage.src}' alt='{enemyImage.alt}' width='64px' height='64px'>
		</div>

	</div>

	<div id='buttons'>
		<button on:click={() => buttonClick('rock')}>Rock</button>
		<button on:click={() => buttonClick('paper')}>Paper</button>
		<button on:click={() => buttonClick('scissors')}>Scissor</button>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	#game {
		display: grid;
		grid-template-columns: repeat(2, auto);
		grid-column-end: span;
	}

	#buttons {
		margin-top: 64px;
	}
</style>
