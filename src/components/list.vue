<template>
  <div class="wrap">
    <ve-line :data="lineData" :colors="lineColors" tooltip-visible legend-visible 
		:width="linewidth" 
		:height="lineheight" :scale="linescale" :settings="lineSettings" class="chart">
        </ve-line>
		<ve-radar :data="radarData" :legend-position="legend_position" :width="radarwidth" :settings="radarSettings"></ve-radar>
  </div>
</template>

<script>
export default {
	data() {
		return {
			lineData: {
				columns: ['日期','专注力', '作息规律', '情绪状况', '活动水平', '礼貌素质'],
				rows: ['日期'],
			},
			lineColors: [],
			linescale: {
				type: Object,
      },
      lineSettings: {
        type: Object
      },
			linewidth: '100%',
			radarwidth: '100%',
      lineheight: '400px',
			legend_position: 'bottom',
			radarData: {
				columns: ['日期','专注力', '作息规律', '情绪状况', '活动水平', '礼貌素质'],
				rows: ['日期'],
			},
			radarSetting: {
				type: Object
			},
			// data: ""
			data: "eyJhbGciOiJIUzI1NiIsImlhdCI6MTU0ODU2MTY0MiwiZXhwIjoxNTY5Mjk3NjQyfQ.eyJpZCI6MSwidXNlcnR5cGUiOiJwYXJlbnQifQ.A8gnpTL2xXfOJTu7rEtqzzK3ulauMahrSOAtkNJY_zE"
		};
	},
	components: {
		VeLine,
		VeRadar
	},

	created() {
		if (window.location.pathname.split('/')[2]) 
			this.data = window.location.pathname.split('/')[2];

		fetch('/api/chart/', {
			headers: {
				'Content-Type': 'application/json',
				'token': this.data
			},
		})
			.then(res => {
				return res.json();
			})
			.then(res => {
				this.lineData = {
					columns: res.chartData.columns,
					rows: res.chartData.rows
				};
				this.radarData = {
					columns: res.chartData.columns,
					rows: res.chartData.rows
				}
			});
		this.lineColors = [
			'#a1b7ec',
			'#5ab1ef',
			'#fa6e86',
			'#ffb980',
			'#0067a6',
			'#c4b4e4',
			'#d87a80',
			'#9cbbff',
			'#d9d0c7',
			'#87a997',
			'#d49ea2',
			'#5b4947',
			'#7ba3a8',
		];
		this.linescale = {
			y: true,
		};
		// this.linewidth = '90%'
		// this.lineheight = '350px'
		this.lineSettings = {
			// xAxisType: 'time',
			area: false,
      nullAddZero: true,
      // metrics: ['日期','专注力', '作息规律', '情绪状况', '活动水平', '礼貌素质'],
      // dimension: ['日期']
		};
		this.radarSettings = {
        dimension: ['日期'],
        metrics: ['专注力', '作息规律', '情绪状况', '活动水平', '礼貌素质'],
				label: {
					position: ['bottom']
				}
      }
	},
};
</script>

<style lang="sass">
.wrap {
	padding-top: 30px;
}
</style>
