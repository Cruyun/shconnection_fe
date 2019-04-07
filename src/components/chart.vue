<template>
  <div class="wrap">
    <ve-line :data="lineData1" :colors="lineColors" tooltip-visible legend-visible 
		:width="linewidth" 
		:height="lineheight" :scale="linescale" :settings="lineSettings" class="chart">
        </ve-line>
		<ve-line :data="lineData2" :colors="lineColors" tooltip-visible legend-visible 
		:width="linewidth" 
		:height="lineheight" :scale="linescale" :settings="lineSettings" class="chart">
        </ve-line>
				<ve-line :data="lineData3" :colors="lineColors" tooltip-visible legend-visible 
		:width="linewidth" 
		:height="lineheight" :scale="linescale" :settings="lineSettings" class="chart">
        </ve-line>
  </div>
</template>

<script>
export default {
	data() {
		return {
			lineData1: {
				columns: [],
				rows: ['日期'],
			},
			lineData2: {
				columns: [],
				rows: ['日期'],
			},
			lineData3: {
				columns: [],
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
		};
	},
	components: {
		VeLine,
	},

	created() {
		fetch('/api/chart/kmeans/', {
			headers: {
				'Content-Type': 'application/json'
			},
		})
			.then(res => {
				return res.json();
			})
			.then(res => {
				this.lineData1 = {
					columns: res.k_datas[0].data.columns,
					rows: res.k_datas[0].data.rows,
				}
				this.lineData2 = {
					columns: res.k_datas[1].data.columns,
					rows: res.k_datas[1].data.rows,
				};
				this.lineData3 = {
					columns: res.k_datas[2].data.columns,
					rows: res.k_datas[2].data.rows,
				};
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
      '#a1b7ec',
			'#5ab1ef',
			'#fa6e86',
			'#ffb980',
			'#0067a6',
			'#c4b4e4',
			'#d87a80'
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
	},
};
</script>

<style lang="sass">
.wrap {
	padding-top: 30px;
}
.chart {
	margin-top: 20px;
}
</style>
