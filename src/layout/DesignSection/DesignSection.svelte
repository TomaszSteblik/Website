<script lang="ts">
	import { links } from "$data/links";

	import { Button, HeaderChip, HyperlinkButton, PageSection } from "$lib";

	let scrollY: number;
</script>

<svelte:window bind:scrollY />

<PageSection id="design-section">
	<HeaderChip>Design</HeaderChip>
	<h2>Power meets beauty.</h2>
	<p>
		Explore a beautiful Windows-first design. Manage all your files with
		increased productivity. Work across multiple folders with tabs. And so much
		more.
	</p>
	<div class="buttons-spacer">
		<Button
			href="https://microsoft.com/store/apps/{links.storeId}"
			rel="noreferrer noopener"
			target="_blank"
			variant="accent"
		>
			Try it out
		</Button>
		<HyperlinkButton
			href="https://www.microsoft.com/design/fluent/"
			rel="noreferrer noopener"
			target="_blank"
		>
			Design System
		</HyperlinkButton>
	</div>
	<div class="design-image">
		<picture>
			<source
				media="(prefers-color-scheme: dark)"
				srcset="/screenshots/folder-list-dark.png"
			/>
			<source
				media="(prefers-color-scheme: light)"
				srcset="/screenshots/folder-list-light.png"
			/>
			<img
				alt="Files folder list screenshot"
				class="files-screenshot"
				height="768"
				src="/screenshots/folder-list-light.png"
				style="transform: translateY({Math.floor(scrollY / -10)}px)"
				width="1024"
			/>
		</picture>
		<picture>
			<source
				media="(prefers-color-scheme: dark)"
				srcset="/screenshots/win11-dark.jpg"
			/>
			<source
				media="(prefers-color-scheme: light)"
				srcset="/screenshots/win11-light.jpg"
			/>
			<img
				alt="Windows 11 wallpaper"
				class="files-wallpaper"
				height="900"
				src="/screenshots/win11-light.jpg"
				width="1440"
			/>
		</picture>
	</div>
</PageSection>

<style lang="scss">
	@use "DesignSection";
</style>
