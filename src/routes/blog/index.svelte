<script context="module" lang="ts">
	import type { Load } from "@sveltejs/kit"

	export const load: Load = async ({ fetch }) => ({
		props: {
			posts: await fetch("/blog.json").then(response => response.json())
		}
	})
</script>

<script lang="ts">
	import { Button, PageSection, HeaderChip, BlogCard, tilt } from "$lib"
	import { page } from "$app/stores";

	interface Post {
		path: string;
		metadata: {
			title: string;
			description: string;
			author: string;
			thumbnail: string;
			date: string;
		};
	}

	export let posts: Post[]

	const mainPost: Post = posts[0]

	let scrollY: number
</script>

<svelte:head>
	<title>Files - Blog</title>
	<meta content="Files - Blog" name="og:title"/>
	<meta content="Files - Blog" name="twitter:title"/>

	<meta content="/branding/banner-blog-light.png" name="og:image"/>
	<meta content="https://{$page.host}/branding/banner-blog-light.png" name="twitter:image"/>
</svelte:head>

<svelte:window bind:scrollY/>

<PageSection id="blog">
	<div class="blog-backdrop">
		<img
				alt=""
				src={mainPost.metadata.thumbnail}
				style="transform: translateY({Math.floor(scrollY / 2.5)}px)"
				width="0"
		/>
	</div>
	<div class="main-post">
		<a href="/blog/{mainPost.path.replace(/\.[^/.]+$/, '')}/">
			<img
					alt="Main post thumbnail"
					height="422"
					src={mainPost.metadata.thumbnail}
					use:tilt={{ max: 2.5, scale: 1.01 }}
					width="633"
			/>
		</a>
		<div class="main-post-info">
			<HeaderChip
			>{new Date(
		  mainPost.metadata.date.replace(/-/g, "/").replace(/T.+/, "")
	  ).toLocaleDateString("en-US", {
		  year: "numeric",
		  day: "numeric",
		  month: "short"
	  })}</HeaderChip
			>
			<h2>{mainPost.metadata.title}</h2>
			<p>{mainPost.metadata.description}</p>
			<Button
					href="blog/{mainPost.path.replace(/\.[^/.]+$/, '')}"
					variant="accent"
			>Read More
			</Button>
		</div>
	</div>
	{#if posts.slice(1).length > 0}
		<div class="blog-cards">
			{#each posts.slice(1) as post}
				<BlogCard path={post.path} {...post.metadata}/>
			{/each}
		</div>
	{:else}
		<p>More posts coming soon!</p>
	{/if}
</PageSection>

<style lang="scss">
	@use "../src/styles/pages/blog";
</style>