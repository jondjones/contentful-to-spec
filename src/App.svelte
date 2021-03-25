<script>
	import Table, { Row } from "@fabiohvp/svelte-table";
	let contentfulJSON = null;
	let rows = null;
	let page = 0;
	function convertToHtml() {
		let items = JSON.parse(contentfulJSON);
		rows = items.fields.map((item) => {
			return {
				componentName: items.name,
				name: item.name,
				type: item.type,
				required: item.required,
				disabled: item.requirdisableded ?? false,
			}
		});
	}

</script>

<style>
	.container {
		height: 90vh;
		margin: 2rem;
		display: grid;
		grid-template-columns: 1fr 4fr;
	}
	
	textarea {
		height: 70vh;
		width: 90%
	}

</style>


<main>
	<div class="container">
		<div class="edit-controls cell">
			<textarea bind:value={contentfulJSON} placeholder="Add Contentful JSON here" />
			<button on:click={convertToHtml}>Convert To HTML table</button>
		</div>
		<div class="table-display cell">
			{#if rows}
			<Table bind:page {rows} >
				<thead slot="head">
				<tr>
					<td><strong>ID</strong></td>
					<td><strong>Label</strong></td>
					<td><strong>Element Type</strong></td>
					<td><strong>Description</strong></td>
					<td><strong>Source</strong></td>
					<td><strong>Is Editable</strong></td>
					<td><strong>Notes</strong></td>
					<td><strong>CMS Mandatory</strong></td>
				</tr>
				</thead>
				<tbody>
				{#each rows as row, index (row)}
					<Row {index}>
					<td>{index}</td>
					<td>{row.name}</td>
					<td>{row.type}</td>
					<td>&nbsp;</td>
					<td>{row.required}</td>
					<td>{row.disabled ? "No" : "Yes"}</td>
					<td>&nbsp;</td>
					<td>{row.disabled}</td>
					</Row>
				{/each}
				</tbody>
			</Table>
			{/if}
		</div>
	</main>

