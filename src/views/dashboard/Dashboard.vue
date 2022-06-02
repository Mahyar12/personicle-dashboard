<template>
	<v-container id="dashboard" fluid tag="section">
		<v-row>
			<v-col cols="12" sm="6" lg="3">
				<base-material-card
					class="v-card-profile"
					avatar="https://demos.creative-tim.com/vue-material-dashboard/img/marc.aba54d65.jpg"
				>
					<v-card-text>
						<h6 class="display-1 mb-1 grey--text">
							{{'Name: Bruce Wayne'}}
						</h6>											
						<h6 class="display-1 mb-1 grey--text">
							{{'Gender: '}}
						</h6>											
						<h6 class="display-1 mb-1 grey--text">
							{{'Age: '}}
						</h6>											
						<h6 class="display-1 mb-1 grey--text">
							{{'Weight: '}}
						</h6>											
						<h6 class="display-1 mb-1 grey--text">
							{{'Height: '}}
						</h6>											
						<h6 class="display-1 mb-1 grey--text">
							{{'Race: '}}
						</h6>											
						<h6 class="display-1 mb-1 grey--text">
							{{'City/Region: '}}
						</h6>											
					</v-card-text>
				</base-material-card>
			</v-col>
			<v-col cols="12" sm="6" lg="9">
				<base-material-card color="#6A887D" title="Scores" class="px-5 py-3">
					<v-row>
						<v-col cols="12" sm="6" lg="6">
							<v-card-text class="text-center">
								<h6 class="display-1 mb-1 grey--text">
									{{'Activity:'}}
								</h6>		
								<h4 class="display-1 mb-1 font-weight-bold">
									{{activity_score}}
								</h4>		
							</v-card-text>
						</v-col>
						<v-col cols="12" sm="6" lg="6">
							<v-card-text class="text-center">
								<h6 class="display-1 mb-1 grey--text">
									{{'Sleep:'}}
								</h6>		
								<h4 class="display-1 mb-1 font-weight-bold">
									{{sleep_score}}
								</h4>		
							</v-card-text>
						</v-col>						
					</v-row>
				</base-material-card>
				<base-material-card color="#6A887D" title="Current Vitals" class="px-5 py-3">
					<v-row>
						<v-col cols="12" sm="4" lg="4">
							<v-card-text class="text-center">
								<h6 class="display-1 mb-1 grey--text">
									{{'Average 24 Hours Heart Rate:'}}
								</h6>		
								<h4 class="display-1 mb-1 font-weight-bold">
									{{avgHR}}
								</h4>		
							</v-card-text>
						</v-col>
						<v-col cols="12" sm="4" lg="4">
							<v-card-text class="text-center">
								<h6 class="display-1 mb-1 grey--text">
									{{'Minimum 2 Weeks Heart Rate:'}}
								</h6>		
								<h4 class="display-1 mb-1 font-weight-bold">
									{{minHR}}
								</h4>		
							</v-card-text>
						</v-col>
						<v-col cols="12" sm="4" lg="4">
							<v-card-text class="text-center">
								<h6 class="display-1 mb-1 grey--text">
									{{'Maximum 2 Weeks Heart Rate:'}}
								</h6>		
								<h4 class="display-1 mb-1 font-weight-bold">
									{{maxHR}}
								</h4>		
							</v-card-text>
						</v-col>						
					</v-row>
				</base-material-card>
			</v-col>			
			<v-col cols="12">
				<base-material-card color="#6A887D" title="Lifestyle Data and Trends" class="px-5 py-3">
					<v-tabs vertical>
						<v-tab style="padding:20px;">
							<v-icon left>
								mdi-power-sleep
							</v-icon>
							Sleep
						</v-tab>
						<v-tab>
							<v-icon left>
								mdi-bike
							</v-icon>
							Activity
						</v-tab>

						<v-tab-item eager>
							<v-card flat>
								<v-card-text>
									<v-row>
										<v-col cols="12" sm="4" lg="4"/>
										<v-col cols="12" sm="6" lg="6">
											<v-btn        
												class="ma-2"
												min-width="0"
												color="indigo"
												outlined
												@click="changeData(0, 0)"
											>
												Daily
											</v-btn>
											<v-btn        
												class="ma-2"
												min-width="0"
												color="indigo"
												outlined
												@click="changeData(0, 1)"
											>
												Weekly
											</v-btn>
										</v-col>
									</v-row>
									<custom-chart :chartData="sleepChart" id="chart" :showLegend="false" />
								</v-card-text>
							</v-card>
						</v-tab-item>
						<v-tab-item eager>
							<v-card flat>
								<v-card-text>
									<v-row>
										<v-col cols="12" sm="4" lg="4"/>
										<v-col cols="12" sm="6" lg="6">
											<v-btn        
												class="ma-2"
												min-width="0"
												color="indigo"
												outlined
												@click="changeData(1, 0)"
											>
												Daily
											</v-btn>
											<v-btn        
												class="ma-2"
												min-width="0"
												color="indigo"
												outlined
												@click="changeData(1, 1)"
											>
												Weekly
											</v-btn>
										</v-col>
									</v-row>
									<custom-chart :chartData="walkChart" id="chart2" :showLegend="false" />
								</v-card-text>
							</v-card>
						</v-tab-item>					
					</v-tabs>
				</base-material-card>
			</v-col>
			<!-- <v-col cols="12" lg="6">
				<base-material-card color="#6A887D" title="Sleep" class="px-5 py-3">
					<custom-chart :chartData="sleepChart" id="chart" :showLegend="false" />
				</base-material-card>
			</v-col>
			<v-col cols="12" lg="6">
				<base-material-card color="#6A887D" title="Walk" class="px-5 py-3" >
					<custom-chart :chartData="walkChart" id="chart2" :showLegend="false" />
				</base-material-card>
			</v-col> -->
		</v-row>
	</v-container>
</template>

<script>
import CustomChart from "./components/Chart.vue";
import axios from 'axios'
import moment from 'moment'

export default {
	name: "DashboardDashboard",
  components: {
		"custom-chart": CustomChart,
	},
	data() {
		return {
			sleepChart: {data: [{data:[], label: 'Duration (hours)', backgroundColor: '#98b8ac'}], labels: []},     
			walkChart: {data: [{data:[], label: 'Steps', backgroundColor: '#98b8ac'}], labels: []},
			sleepChartWeekly: {data: [{data:[], label: 'Duration (hours)', backgroundColor: '#98b8ac'}], labels: []},     
			walkChartWeekly: {data: [{data:[], label: 'Steps', backgroundColor: '#98b8ac'}], labels: []},
			minHR: 200,
			maxHR: 0,
			avgHR: 0,
			activity_score: 0,
			sleep_score: 0,
			sleepConf: -1,
			activityConf: -1
		};
	},
  watch: {
    token() {
			this.calcHR()
      console.log("token changed", this.token)
			this.calcSteps()
			this.calcSleep()
    }
  },
  computed: {
    token: {
      get () {
        return this.$store.state.token
      },
      set (val) {
        this.$store.commit('SET_TOKEN', val)
      },
    },
  },
	mounted() {
		// console.log('token', this.token)
    // this.sleepChart = {data: [{data:[1,2,3], label: 'test', backgroundColor: '#98b8ac'}], labels: ['09/12', '09/13', '09/14']}
    // this.walkChart = {data: [{data:[1,2,3], label: 'test', backgroundColor: '#98b8ac'}], labels: ['09/12', '09/13', '09/14']}
	},
	methods: {
		changeData(chart, status) {
			if(chart == 1) {				
				if(status !== this.activityConf) {
					let tmp = this.walkChart
					this.walkChart = this.walkChartWeekly
					this.walkChartWeekly = tmp
				}
				this.activityConf = status
			}
			else {
				if(status !== this.sleepConf) {
					let tmp = this.sleepChart
					this.sleepChart = this.sleepChartWeekly
					this.sleepChartWeekly = tmp
				}
				this.sleepConf = status
			}
		},
		calcSteps() {
			let start_time = moment().subtract(3, 'months').format('YYYY-MM-DD HH:mm:ss.SSSS')
			let end_time = moment().format('YYYY-MM-DD HH:mm:ss.SSSS')
      axios.get('https://staging.personicle.org/data/read/datastreams?datatype=com.personicle.individual.datastreams.step.count&startTime=' + start_time + '&endTime=' + end_time + '&source=google-fit',
      {
        headers: { Authorization: `Bearer ${this.token}` }
      })
      .then(response => {
				let sdata = {}
				response.data.filter(element=> (moment(element.timestamp) > moment().subtract(2, 'weeks'))).map(element=>{return {...element, timestamp: moment(element.timestamp).startOf('day')}}).forEach(element => {
					if(!!sdata[moment(element.timestamp).format("MM-DD")])
						sdata[moment(element.timestamp).format("MM-DD")] += element.value
					else 
						sdata[moment(element.timestamp).format("MM-DD")] = element.value					
				});

				this.activity_score = (Object.keys(sdata).map(e=>sdata[e]).filter(e=>e>8000).length*1.0/Object.keys(sdata).length).toFixed(2)

				this.walkChartWeekly.data[0].data.push(...Object.keys(sdata).map(e=>sdata[e]))
				this.walkChartWeekly.labels.push(...Object.keys(sdata))
				sdata = {}
				response.data.map(element=>{return {...element, timestamp: moment(element.timestamp).startOf('week')}}).forEach(element => {
					if(!!sdata[moment(element.timestamp).format("MM-DD")])
						sdata[moment(element.timestamp).format("MM-DD")] += element.value
					else 
						sdata[moment(element.timestamp).format("MM-DD")] = element.value
				});
				this.walkChart.data[0].data.push(...Object.keys(sdata).map(e=>sdata[e]))
				this.walkChart.labels.push(...Object.keys(sdata))
				
      })
      .catch((err) => {
        console.log("err", err)
      })
		},
		calcSleep() {
			let start_time = moment().subtract(3, 'months').format('YYYY-MM-DD HH:mm:ss.SSSS')
			let end_time = moment().format('YYYY-MM-DD HH:mm:ss.SSSS')
      axios.get('https://api.personicle.org/data/read/events?startTime=' + start_time + '&endTime=' + end_time + '&source=google-fit',
      {
        headers: { Authorization: `Bearer ${this.token}` }
      })
      .then(response => {
				let sdata = {}
				response.data.filter(element=> (element.event_name=='Sleep' && moment(element.start_time) > moment().subtract(2, 'weeks'))).map(element=>{return {...element, start_time: moment(element.start_time).startOf('day')}}).forEach(element => {
					if(!!sdata[moment(element.start_time).format("MM-DD")])
						sdata[moment(element.start_time).format("MM-DD")] += (element.parameters.duration/3600000.0)
					else 
						sdata[moment(element.start_time).format("MM-DD")] = (element.parameters.duration/3600000.0)
				});

				this.sleep_score = ((Object.keys(sdata).map(e=>sdata[e]).filter(e=>e>8).length*1.0/Object.keys(sdata).length)*100).toFixed(2)

				this.sleepChartWeekly.data[0].data.push(...Object.keys(sdata).map(e=>sdata[e]))
				this.sleepChartWeekly.labels.push(...Object.keys(sdata))
				sdata = {}
				response.data.filter(element=> (element.event_name=='Sleep')).map(element=>{return {...element, start_time: moment(element.start_time).startOf('week')}}).forEach(element => {
					if(!!sdata[moment(element.start_time).format("MM-DD")])
						sdata[moment(element.start_time).format("MM-DD")] += (element.parameters.duration/3600000.0)
					else 
						sdata[moment(element.start_time).format("MM-DD")] = (element.parameters.duration/3600000.0)
				});
				this.sleepChart.data[0].data.push(...Object.keys(sdata).map(e=>sdata[e]))
				this.sleepChart.labels.push(...Object.keys(sdata))
				
      })
      .catch((err) => {
        console.log("err", err)
      })
		},
		calcHR() {
			let start_time = moment().subtract(2, 'weeks').format('YYYY-MM-DD HH:mm:ss.SSSS')
			let end_time = moment().format('YYYY-MM-DD HH:mm:ss.SSSS')
			axios.get('https://api.personicle.org/data/read/datastreams?datatype=com.personicle.individual.datastreams.heartrate&startTime=' + start_time + '&endTime=' + end_time + '&source=google-fit',
				{
					headers: { Authorization: `Bearer ${this.token}` }
				})
				.then(response => {					
					let count = 0
					let avg = 0
					response.data.forEach(element => {
						if(moment(element.timestamp) >= moment().subtract(1, 'day')) {
							count++
							avg += element.value
						}
						if(element.value > this.maxHR)
							this.maxHR = element.value
						if(element.value < this.minHR)
							this.minHR = element.value
					});
					if(count == 0)
						this.avgHR = (this.minHR + this.maxHR)/2
					else
						this.avgHR = avg/count
				})
				.catch((err) => {
					console.log("err", err)
				})
		},
		complete(index) {
			this.list[index] = !this.list[index];
		},
	},
};
</script>
