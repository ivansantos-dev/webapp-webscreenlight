<script lang="ts">
	import { onMount } from 'svelte';
	onMount(() => {
		document.body.style.backgroundColor = '#ffffff';
	});
	const requestFullScreen = () => {
		// Supports most browsers and their versions.
		let element = document.getElementsByClassName('box')[0];
		element.style.backgroundColor = document.body.style.backgroundColor;
		var requestMethod =
			element.requestFullScreen ||
			element.webkitRequestFullScreen ||
			element.mozRequestFullScreen ||
			element.msRequestFullScreen;

		if (requestMethod) {
			// Native full screen.
			requestMethod.call(element);
		} else if (typeof window.ActiveXObject !== 'undefined') {
			// Older IE.
			var wscript = new ActiveXObject('WScript.Shell');
			if (wscript !== null) {
				wscript.SendKeys('{F11}');
			}
		}
	};
</script>

<div class="container">
	<header
		class="d-flex flex-wrap align-items-center justify-content-center justify-content-md-between py-3 mb-4 border-bottom"
	>
		<a href="/" class="text-dark text-decoration-none"><h1>Web Monitor Light</h1></a>

		<ul class="nav col-12 col-md-auto mb-2 justify-content-center mb-md-0">
			<li class="nav-item">
				<a href="/" class="nav-link">Home</a>
			</li>
			<li class="nav-item">
				<a href="#" data-bs-toggle="modal" data-bs-target="#exampleModal" class="nav-link">FAQ</a>
			</li>

			<li class="nav-item"><a href="/credits" class="nav-link">Credits</a></li>
			<li class="nav-item">
				<a href="#" on:click={requestFullScreen} class="nav-link">Go Fullscreen</a>
			</li>
		</ul>
	</header>
	<main>
		<slot />
	</main>
	<div class="container fixed-bottom">
		<footer
			class="d-flex flex-wrap justify-content-between align-items-center py-3 my-4 border-top"
		>
			<p class="col-md-4 mb-0 text-muted">
				&copy; 2022 <a href="http://ivan-santos.dev" target="_blank" class="text-decoration-none"
					>Ivan Santos</a
				>
			</p>
		</footer>
	</div>
</div>

<div
	class="modal fade"
	id="exampleModal"
	tabindex="-1"
	aria-labelledby="exampleModalLabel"
	aria-hidden="true"
>
	<div class="modal-dialog">
		<div class="modal-content">
			<div class="modal-header">
				<h5 class="modal-title">FAQ</h5>
				<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" />
			</div>
			<div class="modal-body">
				<p><strong>Web Monitor Light</strong> is a simple tool to light whatever you need.</p>

				<p>Use-cases:</p>
				<ul>
					<li>source of light for videos</li>
					<li>background light to copy drawing</li>
					<li>black your screen in order to clean it</li>
					<li>test monitor</li>
				</ul>
			</div>
		</div>
	</div>
</div>
<div class="box" />

<style>
	.box {
		background-color: red;
		width: 0px;
		height: 0px;
	}
</style>
