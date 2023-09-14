<script>
	let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

	let spiritboxLocation = () => {
		console.log("i am behind you >:3");
	}

	let spiritboxAge = () => {
		console.log("i am very old and my bones hurt");
	}

	let spiritboxFriendliness = () => {
		console.log("i will hunt you lmao")
	}
</script>

<button on:click={spiritboxLocation}>Where are you?</button>
<button on:click={spiritboxAge}>How old are you?</button>
<button on:click={spiritboxFriendliness}>Are you friendly?</button>