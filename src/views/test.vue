<template lang="pug">
	.test
		data-table(
			:header-items="headerItems"
			:items="items"
		)
			template(#column-offRoad="{ value }")
				input(type="radio" :checked="value" disabled)
			template(#column-color="{ value }")
				span.color-block(:style="{ 'background-color': value }")
			template(#column-popularity="{ value }")
				span.popularity__wrap
					span.color-block.green(:style="{ width: `${value}%` }") {{ value }} %
</template>
<script lang="ts">
	import { Component, Vue } from 'vue-property-decorator';
	import DataTable from '@/components/table.vue';

	@Component({
		components: { DataTable },
	})
	export default class Test extends Vue {
		headerItems = [
			{
				text: 'Марка автомобиля',
				value: 'name',
			},
			{
				text: 'Объем двигателя',
				value: 'volume',
			},
			{
				text: 'Максимальная скорость',
				value: 'maxSpeed',
			},
			{
				text: 'Внедорожник',
				value: 'offRoad',
				slot: true,
			},
			{
				text: 'Цвет кузова',
				value: 'color',
				slot: true,
			},
			{
				text: 'Цена $',
				value: 'prise',
			},
			{
				text: 'Популярность (1-100%)',
				value: 'popularity',
				slot: true,
			},
		];

		items = [
			{
				name: 'BMW m3',
				volume: 2.5,
				maxSpeed: 230,
				color: 'black',
				prise: 100000,
				popularity: '70',
				offRoad: false,
			},
			{
				name: 'Honda civic',
				volume: 1.6,
				maxSpeed: 180,
				color: 'yellow',
				prise: 40000,
				popularity: '40',
				offRoad: false,
			},
			{
				name: 'ZAZ 968',
				volume: 0.8,
				maxSpeed: 110,
				color: 'orange',
				prise: 1000,
				popularity: '100',
				offRoad: true,
			},
			{
				name: 'Lamborghini Aventador',
				volume: 6.5,
				maxSpeed: 350,
				color: 'red',
				prise: 1500000,
				popularity: '30',
				offRoad: false,
			}
		];
	}
</script>
<style lang="stylus">
.color-block
	display inline-block
	width 20px
	height 20px
	color black
	&.green
		background-color green

.popularity
	&__wrap
		display block
		height 20px
</style>
