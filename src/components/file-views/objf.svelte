<script lang="ts">
	import type {ObjfContent} from 'dbpf-transform/dist/esm/types';
	import produce from 'immer';
	import Box from '../box.svelte';
	import {formatHex} from '../../util';

	export let content: ObjfContent;
	export let onChange: () => void;

	const FNS = [
		'init',
		'main',
		'load',
		'cleanup',
		'queue skipped',
		'allow intersection',
		'wall adjacency changed',
		'room changed',
		'dynamic multi-tile update',
		'placement',
		'pickup',
		'user placement',
		'user pickup',
		'level info request',
		'serving surface',
		'portal',
		'gardening',
		'wash hands',
		'prep',
		'cook',
		'surface',
		'dispose',
		'food',
		'pickup from slot',
		'wash dish',
		'eating surface',
		'sit',
		'stand',
		'clean',
		'repair',
		'ui event',
		'Restock',
		'Wash Clothes',
		'start live mode',
		'stop live mode',
		'link objects',
		'message handler',
		'pre route',
		'post route',
		'goal check',
		'reaction handler',
		'along route callback',
		'awareness',
		'reset',
		'look at target',
		'walk over',
		'utility state change',
		'set model by type',
		'get model type',
		'delete',
		'user delete',
		'just moved in',
		'prevent place in slot',
		'global awareness',
		'object updated by design mode',
	];
</script>

<div>
	<Box secondary>
		<table>
			<thead>
				<td>Function</td>
				<td>Action BHAV</td>
				<td>Guardian BHAV</td>
			</thead>
			<tbody>
			{#each content.functions as fn, i}
				<tr>
					<td>{FNS[i]}</td>
					<td>
						<input
							type="text"
							placeholder="none"
							value={formatHex(fn.action || undefined, 4)}
							on:input={(e) => onChange(
								produce(content, (draft) => {
									draft.functions[i].action = parseInt(e.target.value, 16);
								})
							)}
						/>
					</td>
					<td>
						<input
							type="text"
							placeholder="none"
							value={formatHex(fn.guardian || undefined, 4)}
							on:input={(e) => onChange(
								produce(content, (draft) => {
									draft.functions[i].guardian = parseInt(e.target.value, 16);
								})
							)}
						/>
					</td>
				</tr>
			{/each}
			</tbody>
		</table>
	</Box>
</div>

<style>
	div {
		height: 100%;
		overflow: auto;
	}
	table {
		width: 100%;
		border-collapse: collapse;
	}
	thead {
		border-bottom: 1px solid var(--color-accent);
	}
	thead td {
		padding-bottom: 10px;
	}
	td {
		padding-top: 10px;
		font-size: 1rem;
	}
	td:not(:last-child) {
		padding-right: 10px;
	}
	input {
		width: 100%;
	}
</style>
