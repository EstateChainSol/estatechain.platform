<script lang="ts">
	import '../app.css';
	import { base } from '$app/paths';
	let isMenuOpen = false;
</script>

<div class="min-h-screen bg-gradient-to-br from-gray-900 to-black text-white">
	<!-- Demo Banner -->
	<div
		class="sticky top-0 z-50 bg-gradient-to-r from-blue-600/10 to-purple-600/10 border-b border-blue-500/20 backdrop-blur-lg"
	>
		<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-2 text-center text-sm">
			<span class="bg-blue-500/20 text-blue-300 px-2 py-1 rounded-md font-medium mr-2"
				>Preview Version</span
			>
			<span class="text-gray-300"
				>This is a design preview. Features are simulated for demonstration purposes.</span
			>
		</div>
	</div>

	<nav class="sticky top-8 w-full bg-black/30 backdrop-blur-lg border-b border-gray-800 z-40">
		<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
			<div class="flex justify-between h-16">
				<div class="flex items-center">
					<a href="{base}/" class="flex items-center space-x-2">
						<span
							class="text-2xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-600"
							>EstateChain</span
						>
					</a>
				</div>

				<div class="hidden md:flex items-center space-x-8">
					<a href="{base}/portfolio" class="text-gray-300 hover:text-white transition-colors">Portfolio</a
					>
					<a href="{base}/marketplace" class="text-gray-300 hover:text-white transition-colors"
						>Marketplace</a
					>
					<a href="{base}/governance" class="text-gray-300 hover:text-white transition-colors"
						>Governance</a
					>
					<button
						class="group relative px-4 py-2 rounded-lg bg-gradient-to-r from-blue-500/50 to-purple-600/50 hover:from-blue-600/50 hover:to-purple-700/50 transition-all"
					>
						<span class="relative z-10 group-hover:opacity-0 transition-opacity"
							>Connect Wallet</span
						>
						<span
							class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity"
						>
							Demo Only
						</span>
					</button>
				</div>

				<button
					class="md:hidden p-2"
					on:click={() => (isMenuOpen = !isMenuOpen)}
					aria-label={isMenuOpen ? 'Close menu' : 'Open menu'}
				>
					<svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d={isMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'}
						/>
					</svg>
				</button>
			</div>
		</div>

		{#if isMenuOpen}
			<div class="md:hidden">
				<div class="px-2 pt-2 pb-3 space-y-1">
					<a
						href="{base}/portfolio"
						class="block px-3 py-2 text-gray-300 hover:text-white transition-colors">Portfolio</a
					>
					<a
						href="{base}/marketplace"
						class="block px-3 py-2 text-gray-300 hover:text-white transition-colors">Marketplace</a
					>
					<a
						href="{base}/governance"
						class="block px-3 py-2 text-gray-300 hover:text-white transition-colors">Governance</a
					>
					<button
						class="group relative w-full mt-2 px-4 py-2 rounded-lg bg-gradient-to-r from-blue-500/50 to-purple-600/50 hover:from-blue-600/50 hover:to-purple-700/50 transition-all"
					>
						<span class="relative z-10 group-hover:opacity-0 transition-opacity"
							>Connect Wallet</span
						>
						<span
							class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity"
						>
							Demo Only
						</span>
					</button>
					<p class="mt-4 px-3 py-2 text-sm text-gray-400 border-t border-gray-800">
						This is a design preview with simulated features.
					</p>
				</div>
			</div>
		{/if}
	</nav>

	<main class="pt-16 min-h-screen">
		<slot />
	</main>

	<footer class="bg-black/30 backdrop-blur-lg border-t border-gray-800">
		<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
			<div class="grid grid-cols-1 md:grid-cols-3 gap-8">
				<div>
					<h3 class="text-lg font-semibold mb-4">EstateChain</h3>
					<p class="text-gray-400">
						Democratizing real estate investment through blockchain technology.
					</p>
				</div>
				<div>
					<h3 class="text-lg font-semibold mb-4">Resources</h3>
					<ul class="space-y-2 text-gray-400">
						<li><a href="https://estatechainsol.github.io/estatechain.docs" target="_blank" class="hover:text-white transition-colors">Documentation</a></li>
						<li><a href="{base}/faq" class="hover:text-white transition-colors">FAQ</a></li>
					</ul>
				</div>
				<div>
					<h3 class="text-lg font-semibold mb-4">Connect</h3>
					<ul class="space-y-2 text-gray-400">
						<li>
							<a href="https://twitter.com/realtokens" class="hover:text-white transition-colors"
								>Twitter</a
							>
						</li>
					</ul>
				</div>
			</div>
			<div class="mt-8 pt-8 border-t border-gray-800 text-center text-gray-400">
				<p>&copy; 2024 EstateChain. All rights reserved.</p>
			</div>
		</div>
	</footer>
</div>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		font-family:
			system-ui,
			-apple-system,
			BlinkMacSystemFont,
			'Segoe UI',
			Roboto,
			Oxygen,
			Ubuntu,
			Cantarell,
			'Open Sans',
			'Helvetica Neue',
			sans-serif;
	}
</style>
