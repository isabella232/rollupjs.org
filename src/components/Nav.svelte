<script>
	export let page = '';
	let open = false;
	let nav;

	function toggleOpen() {
		// if the menu is closing, scroll back to the top *after* it
		// shuts. otherwise, scroll back to the top immediately
		// (just in case the user reopened before it happened).
		// The reason we don't just do it when the menu opens is
		// that the scrollbar visibly flashes
		if (open) {
			setTimeout(() => {
				if (!open) {
					nav.scrollTop = 0;
				}
			}, 350);
		} else {
			nav.scrollTop = 0;
		}

		open = !open;
	}
</script>

<style>
	.mousecatcher {
		position: fixed;
		left: 0;
		top: 0;
		width: 100vw;
		height: 100vh;
		background-color: black;
		pointer-events: none;
		opacity: 0;
		/*transition: opacity 0.4s;*/
		z-index: 3;
	}

	.mousecatcher.open {
		pointer-events: all;
		opacity: 0.3;
	}

	@keyframes fadein {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	.container {
		position: fixed;
		top: 0;
		width: 100%;
		height: 3em;
		background-color: #f9f9f9;
		color: #222;
		border-bottom: 1px solid #eee;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif,
			'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
		z-index: 5;
	}

	nav {
		position: fixed;
		width: 18em;
		height: calc(100vh - 3em);
		top: 3em;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif,
			'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
		background-color: white;
		transform: translate(-100%, 0);
		transition: transform 0.2s cubic-bezier(0.17, 0.67, 0.24, 0.99);
		border-right: 1px solid #eee;
		z-index: 5;
		padding: 1em;
		user-select: none;
		overflow-y: auto;
	}

	.open {
		transform: translate(0, 0);
		transition: transform 0.3s cubic-bezier(0.17, 0.67, 0.24, 0.99);
	}

	.menu-link {
		display: inline;
		position: absolute;
		top: 0;
		left: 1rem;
		font-size: 1em;
		line-height: 3.1em;
		color: #ccc;
		cursor: pointer;
		font-weight: 500;
		-webkit-tap-highlight-color: transparent;
		-webkit-touch-callout: none;
	}

	.logo {
		position: absolute;
		right: 0.5rem;
		top: 0;
		background-image: url(/logo.svg);
		background-repeat: no-repeat;
		background-position: 100% 50%;
		background-size: auto 80%;
		padding: 1rem 2.2rem 1rem 0;
		line-height: 1;
		color: #222;
		font-weight: 500;
	}

	ul {
		display: block;
		margin: 0;
		padding: 0;
		list-style: none;
	}

	.primary {
		margin: 0 0 2em 0;
	}

	.primary li {
		position: relative;
		display: block;
	}

	.primary .active {
		color: #333;
		font-weight: 700;
	}

	/**/

	.primary li a {
		display: block;
		color: #727272;
		font-size: 1.3em;
		font-weight: 500;
		padding: 0.75em 0;
		line-height: 1;
	}

	@media (min-width: 768px) {
		.mousecatcher,
		.menu-link {
			display: none;
		}

		.container {
			height: 3.6em;
		}

		nav {
			width: 100%;
			height: 4em;
			padding: 0 1.5em 0 0;
			transform: none;
			transition: none;
			height: 0;
			overflow: visible;
		}

		.primary {
			position: fixed;
			top: 0;
			right: 1em;
			margin: 0;
		}

		.primary li {
			display: inline-block;
		}

		.primary li a {
			padding: 1.3em 0.5em;
			color: #666;
			font-size: 1rem;
			font-weight: 300;
		}

		.primary li a.active {
			color: #333;
			font-weight: 500;
		}

		.primary li::after {
			position: absolute;
			top: 1.4rem;
			right: -0.3em;
			content: '/';
			font-size: 0.8em;
			color: #999;
		}

		.primary li:last-child::after {
			content: '';
		}

		.logo {
			position: absolute;
			top: 0;
			left: 0.5rem;
			right: auto;
			padding: 1rem 0 1rem 3rem;
			font-size: 1.6rem;
			font-weight: 300;
			transform: none;
			background-position: 0 50%;
		}
	}
</style>

<div
	class="{open ? 'open' : 'closed'} mousecatcher"
	on:click="{() => {
		open = false;
	}}"></div>

<div class="container">
	<span class="menu-link" on:click="{toggleOpen}">{open ? 'Close' : 'Menu'}</span>

	<a rel="prefetch" href="guide/en/" class="logo">rollup.js</a>
</div>

<nav
	bind:this="{nav}"
	class="{open ? 'open' : 'closed'}"
	on:click="{() => {
		open = false;
	}}">
	<ul class="primary">
		<li><a rel="prefetch" class="{page === 'guide' ? 'active' : ''}" href="guide/en/">guide</a></li>
		<li><a rel="prefetch" class="{page === 'repl' ? 'active' : ''}" href="repl/">repl</a></li>
		<li><a href="https://is.gd/rollup_chat">chat</a></li>
		<li><a href="https://github.com/rollup/rollup">github</a></li>
	</ul>
</nav>
