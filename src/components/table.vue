<template lang="pug">
	table.table
		thead.table__heading
			tr.table__row
				th.table__cell.table__cell_head(
					v-for="headItem in headerItems"
					:key="headItem.value"
					v-text="headItem.text"
				)
		tbody
			tr.table__row(
				v-for="(obj, index) in items"
				:key="`${obj}-${index}`"
			)
				td.table__td(
					v-for="column in headerItems"
				)
					slot(
						v-if="column.slot"
						:name="`column-${column.value}`"
						:value="obj[column.value]"
					)
					span(
						v-else
						v-text="obj[column.value]"
					)
</template>
<script lang="ts">
	import { Component, Vue, Prop } from 'vue-property-decorator';

	interface IHeaderItem {
	  text: string;
	  value: string;
  }

  interface IItems {
	  [key: string]: string | number;
  }

	@Component
	export default class Table extends Vue {
	  @Prop({ type: Array, required: true }) headerItems!: IHeaderItem[];
	  @Prop({ type: Array, required: true }) items!: IItems[];
	}
</script>
<style lang="stylus">
	.table
		&__td
			text-align left
</style>