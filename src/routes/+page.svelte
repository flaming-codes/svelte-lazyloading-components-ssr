<script lang="ts">
	import {
		Alert,
		CardPlaceholder,
		ImagePlaceholder,
		ListPlaceholder,
		Skeleton,
		TestimonialPlaceholder,
		TextPlaceholder,
		VideoPlaceholder,
		WidgetPlaceholder,
		Modal,
		Button
	} from 'flowbite-svelte';

	import type { PageData } from './$types';

	export let data: PageData;

	let defaultModal;

	$: ({ list, container } = data);
</script>

<section class="block p-4 m-6">
	<h2>Home</h2>

	{#if !container}
		<Skeleton />
	{:else}
		{#each list as component}
			{#if container[component.comp]?.default}
				<svelte:component
					this={container[component.comp].default}
					customProp={container[component.comp].props}
				/>
			{/if}
		{/each}
	{/if}
	<Button on:click={() => (defaultModal = true)}>Default modal</Button>
	<Modal title="Terms of Service" bind:open={defaultModal}>
		<p class="text-base leading-relaxed text-gray-500 dark:text-gray-400">
			With less than a month to go before the European Union enacts new consumer privacy laws for
			its citizens, companies around the world are updating their terms of service agreements to
			comply.
		</p>
		<p class="text-base leading-relaxed text-gray-500 dark:text-gray-400">
			The European Union’s General Data Protection Regulation (G.D.P.R.) goes into effect on May 25
			and is meant to ensure a common set of data rights in the European Union. It requires
			organizations to notify users as soon as possible of high-risk data breaches that could
			personally affect them.
		</p>
		<svelte:fragment slot="footer">
			<Button>I accept</Button>
			<Button color="alternative">Decline</Button>
		</svelte:fragment>
	</Modal>
</section>
