<script>
	import TabWrapper from '../../lib/components/tab-wrapper.svelte'
	import { TabAnchor } from '@skeletonlabs/skeleton'
	import { fade } from "svelte/transition"
	import { page } from '$app/stores'
    import { onMount } from "svelte"

	let tabs=[
		['Streaming App', 'streaming-app'],
		['Twitch Bot', 'twitch-bot'],
		['Visual Art', 'visual-art'],
	]

	let tabSet

    onMount(() => {
		tabSet = $page.url.pathname.replace(/.*\/([^/]+)$/, "$1")
		console.log(tabSet)
		if (tabSet === 'portfolio') tabSet = tabs[0][1]
	})
	// try to fix the tab bug
	$: tabSet = $page.url.pathname.replace(/.*\/([^/]+)$/, "$1")

</script>

<div class="quote-container @container" in:fade>
    <div class="quote">project portfolio</div>
</div>

<div class="page-main" id="page-main">
	<TabWrapper listBG="variant-glass-tertiary" panelBG="bg-tertiary-900">
		{#each tabs as [name, slug]}
			<TabAnchor
				href={`/portfolio/${slug}`}
				selected={tabSet === slug}
				on:click={() => tabSet=slug}
			>
				<span>{name}</span>
			</TabAnchor>
		{/each}
		<TabAnchor href="https://wstrother.github.io/devblog/">
			<span>Dev Blog</span>
		</TabAnchor>
		
		<svelte:fragment slot="panel">
			<slot />
		</svelte:fragment>
	</TabWrapper>
</div>
