<template>
	<canvas :id="id" />
</template>

<script>
import Chart from "chart.js";

export default {
	props: {
		chartData: {
			type: Object,
			default: () => {},
		},
		chartType: {
			type: String,
			default: "bar",
		},
		id: {
			type: String,
			default: "chart",
		},
		showLegend: {
			type: Boolean,
			default: true,
		},
	},
	data() {
		return {
			chartObj: {},
		};
	},
	computed: {},
	watch: {
		chartData: {
			handler() {
				console.log("chart change");
				this.updateChart();
			},
		},
	},
	methods: {
		updateChart() {
			console.log("hereeee chart");
			this.chartObj.data.labels = this.chartData.labels;
			this.chartObj.data.datasets = this.chartData.data;
			this.chartObj.update();
		},
		mountChart() {
			const chart = document.getElementById(this.id);
			this.chartObj = new Chart(chart, {
				type: this.chartType,
				data: {
					labels: [],
					datasets: [
						{
							label: "",
							data: [],
							borderWidth: 1,
						},
					],
				},
				options: this.chartType == "horizontalBar" ? {
						scaleShowValues: true,
					 	maintainAspectRatio: false,
						scales: {
							yAxes: [{
								ticks: {
									autoSkip: false
								}
							}]
						}}: {
					responsive: true,
					scales: this.chartType == "bar" ?{
						yAxes: [
							{
								ticks: {
									beginAtZero: true,
								},
							},
						],
					} : {},
					legend: this.showLegend
						? {
								position: "bottom",
								labels: {
									generateLabels: function (chart) {
										var data = chart.data;
										if (
											!!data &&
											data?.labels?.length &&
											data?.datasets?.length
										) {
											return data.labels.map(function (label, i) {
												var meta = chart.getDatasetMeta(0);
												var ds = data.datasets[0];
												var arc = meta.data[i];
												var custom = (arc && arc.custom) || {};
												var getValueAtIndexOrDefault =
													Chart.helpers.getValueAtIndexOrDefault;
												var arcOpts = chart.options.elements.arc;
												var fill = custom.backgroundColor
													? custom.backgroundColor
													: getValueAtIndexOrDefault(
															ds.backgroundColor,
															i,
															arcOpts.backgroundColor
													  );
												var stroke = custom.borderColor
													? custom.borderColor
													: getValueAtIndexOrDefault(
															ds.borderColor,
															i,
															arcOpts.borderColor
													  );
												var bw = custom.borderWidth
													? custom.borderWidth
													: getValueAtIndexOrDefault(
															ds.borderWidth,
															i,
															arcOpts.borderWidth
													  );

												// We get the value of the current label
												var value =
													chart.config.data.datasets[arc._datasetIndex].data[
														arc._index
													];

												return {
													// Instead of `text: label,`
													// We add the value to the string
													text: label + " : " + (value ?? 0),
													fillStyle: fill,
													strokeStyle: stroke,
													lineWidth: bw,
													hidden: isNaN(ds.data[i]) || meta.data[i].hidden,
													index: i,
												};
											});
										} else {
											return [];
										}
									},
								},
						  }
						: {},
				},
			});
		},
	},
	mounted() {
		this.mountChart();
	},
};
</script>


