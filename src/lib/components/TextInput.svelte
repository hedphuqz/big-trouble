<script lang="ts">
	interface Props {
		title?: string;
		value?: string;
		placeholder?: string;
		name?: string;
		id?: string;
		disabled?: boolean;
		maxlength?: number;
	}

	let {
		title = '',
		value = $bindable(''),
		placeholder = '',
		name = '',
		id = '',
		disabled = false,
		maxlength
	}: Props = $props();
</script>

<div class="flex flex-col gap-1">
	{#if title}
		<label for={id} class=" font-family-space font-semibold  tracking-wider mb-0.5 text-xl" >
           {title}
		</label>
	{/if}
	<input
		type="text"
		{id}
		{name}
		{placeholder}
		{disabled}
		{maxlength}
		bind:value
		class="font-family-space text-sm px-3 py-2 border-2 border-gray-500 bg-white text-black shadow-[inset_2px_2px_0_rgba(0,0,0,0.2),inset_-2px_-2px_0_rgba(255,255,255,0.8)] transition-all duration-100 outline-none focus:border-gray-600 focus:shadow-[inset_2px_2px_0_rgba(0,0,0,0.3),inset_-2px_-2px_0_rgba(255,255,255,0.9),0_0_0_2px_rgba(102,102,102,0.2)] disabled:bg-gray-300 disabled:text-gray-500 disabled:cursor-not-allowed disabled:shadow-[inset_1px_1px_0_rgba(0,0,0,0.1),inset_-1px_-1px_0_rgba(255,255,255,0.5)] placeholder:text-gray-500 placeholder:opacity-70"
	/>
</div>