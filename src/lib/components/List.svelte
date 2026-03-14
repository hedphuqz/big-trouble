<script lang="ts">
	import { onMount } from 'svelte';

	interface ListItem {
		date: string;
		label: string;
	}

	interface Props {
		title: string;
		items: ListItem[];
		animate?: boolean;
		typeSpeed?: number; // milliseconds per character
		initialDelay?: number; // milliseconds before starting
	}

	let { title, items, animate = false, typeSpeed = 50, initialDelay = 0 }: Props = $props();

	let displayedTitle = $state('');
	let displayedItems = $state<Array<{ text: string; isComplete: boolean }>>([]);

	async function typeText(
		text: string,
		onUpdate: (partial: string) => void,
		delay: number = 0
	): Promise<void> {
		if (delay > 0) {
			await new Promise((resolve) => setTimeout(resolve, delay));
		}

		for (let i = 0; i <= text.length; i++) {
			onUpdate(text.slice(0, i));
			if (i < text.length) {
				await new Promise((resolve) => setTimeout(resolve, typeSpeed));
			}
		}
	}

	async function animateContent() {
		if (!animate) {
			displayedTitle = title;
			displayedItems = items.map((item) => ({
				text: `${item.date} ${item.label}`,
				isComplete: true
			}));
			return;
		}

		displayedTitle = '';
		displayedItems = [];

		// Type out title
		await typeText(
			title,
			(partial) => {
				displayedTitle = partial;
			},
			initialDelay
		);

		// Type out each item character by character
		for (let i = 0; i < items.length; i++) {
			const itemText = `${items[i].date} ${items[i].label}`;
			
			// Add a new item slot
			displayedItems = [...displayedItems, { text: '', isComplete: false }];
			
			// Type it out character by character
			await typeText(itemText, (partial) => {
				displayedItems = displayedItems.map((item, idx) =>
					idx === i ? { text: partial, isComplete: false } : item
				);
			});
			
			// Mark as complete
			displayedItems = displayedItems.map((item, idx) =>
				idx === i ? { ...item, isComplete: true } : item
			);
		}
	}

	onMount(() => {
		animateContent();
	});
</script>

<div class="font-family-space">
	<h2 class="text-xl font-bold mb-3 ">{displayedTitle}</h2>
	<ul class="list-none p-0 m-0">
		{#each displayedItems as item}
			<li class="mb-2 ">
				{item.text}
			</li>
		{/each}
	</ul>
</div>