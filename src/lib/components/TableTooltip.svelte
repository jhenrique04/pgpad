<script lang="ts">
	import type { TableInfo } from '$lib/commands.svelte';

	let { table }: { table: TableInfo } = $props();

	let schemaPrefix = $derived(!table.schema || table.schema === 'public' ? '' : `${table.schema}.`);
</script>

<div
	class="cm-tooltip-cursor max-h-[250px] overflow-y-auto rounded px-3 py-2 font-[inherit] text-xs"
>
	<div class="mb-1.5 border-b border-gray-500/30 pb-1 font-semibold">
		Table: {schemaPrefix}{table.name}
	</div>

	<div class="flex flex-col gap-1">
		{#each table.columns as col (col.name)}
			<div class="flex justify-between gap-6">
				<span class="font-medium">{col.name}</span>
				<span class="opacity-70">
					{col.data_type}{col.is_nullable ? '' : ' NOT NULL'}
				</span>
			</div>
		{/each}
	</div>
</div>
