<template>
	<v-container id="dashboard" fluid tag="section">
		<v-row>
			<v-col cols="12" sm="6" lg="2">
				<base-material-card
					class="v-card-profile"
					avatar="https://demos.creative-tim.com/vue-material-dashboard/img/marc.aba54d65.jpg"
				>
					<v-card-text>
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
			<v-col cols="12" sm="6" lg="10">
				<base-material-card color="#6A887D" title="Scores" class="px-5 py-3">
					<v-row>
						<v-col cols="12" sm="3" lg="2">
							<v-card-text class="text-center">
								<h6 class="display-1 mb-1 grey--text">
									{{'Activity:'}}
								</h6>		
								<h4 class="display-1 mb-1 font-weight-bold">
									{{'100'}}
								</h4>		
							</v-card-text>
						</v-col>
						<v-col cols="12" sm="3" lg="2">
							<v-card-text class="text-center">
								<h6 class="display-1 mb-1 grey--text">
									{{'Sleep:'}}
								</h6>		
								<h4 class="display-1 mb-1 font-weight-bold">
									{{'100'}}
								</h4>		
							</v-card-text>
						</v-col>
						<v-col cols="12" sm="3" lg="2">
							<v-card-text class="text-center">
								<h6 class="display-1 mb-1 grey--text">
									{{'Readiness:'}}
								</h6>		
								<h4 class="display-1 mb-1 font-weight-bold">
									{{'100'}}
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
			<!-- <v-col cols="12" sm="6" lg="3">
				<base-material-stats-card
					color="info"
					icon="mdi-twitter"
					title="Followers"
					value="+245"
					sub-icon="mdi-clock"
					sub-text="Just Updated"
				/>
			</v-col>

			<v-col cols="12" sm="6" lg="3">
				<base-material-stats-card
					color="primary"
					icon="mdi-poll"
					title="Website Visits"
					value="75.521"
					sub-icon="mdi-tag"
					sub-text="Tracked from Google Analytics"
				/>
			</v-col>

			<v-col cols="12" sm="6" lg="3">
				<base-material-stats-card
					color="success"
					icon="mdi-store"
					title="Revenue"
					value="$ 34,245"
					sub-icon="mdi-calendar"
					sub-text="Last 24 Hours"
				/>
			</v-col>

			<v-col cols="12" sm="6" lg="3">
				<base-material-stats-card
					color="orange"
					icon="mdi-sofa"
					title="Bookings"
					value="184"
					sub-icon="mdi-alert"
					sub-icon-color="red"
					sub-text="Get More Space..."
				/>
			</v-col> -->
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
			sleepChart: {data: [{data:[], label: 'duration', backgroundColor: '#98b8ac'}], labels: []},     
			walkChart: {data: [{data:[], label: 'duration', backgroundColor: '#98b8ac'}], labels: []},
			sleepChartWeekly: {data: [{data:[], label: 'duration', backgroundColor: '#98b8ac'}], labels: []},     
			walkChartWeekly: {data: [{data:[], label: 'duration', backgroundColor: '#98b8ac'}], labels: []},
			minHR: 200,
			maxHR: 0,
			avgHR: 0,
			sleepConf: -1,
			activityConf: -1
		};
	},
  watch: {
    token() {
			this.calcHR()
      console.log("token changed", this.token)
			this.calcSteps()

			// axios.get('https://api.personicle.org/data/read/events?datatype=com.personicle.individual.datastreams.step.cadence&startTime=2021-12-25%2018:48:08.872234&endTime=2022-03-25%2013:48:08.872460&source=google-fit',
      // {
      //   headers: { Authorization: `Bearer ${this.token}` }
      // })
      // .then(response => {
      //   console.log("resp", response)
			// 	response.data.forEach(element => {
			// 		if(element.event_name == "Sleep") {
			// 			this.sleepChart.data[0].data.push(element.parameters.duration)
			// 			this.sleepChart.labels.push(new moment(element.start_time).format("MM-DD HH:mm"))
			// 		}
			// 	});
			// 	console.log("walk", this.walkChart)
      // })
      // .catch((err) => {
      //   console.log("err", err)
      // })
			
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
			else 
				this.sleepConf = status
		},
		calcSteps() {
			let start_time = moment().subtract(3, 'months').format('YYYY-MM-DD HH:mm:ss.SSSS')
			let end_time = moment().format('YYYY-MM-DD HH:mm:ss.SSSS')
      axios.get('https://staging.personicle.org/data/read/datastreams?datatype=com.personicle.individual.datastreams.step.count&startTime=' + start_time + '&endTime=' + end_time + '&source=google-fit',
      {
        headers: { Authorization: `Bearer ${this.token}` }
      })
      .then(response => {
        console.log("resp", response)
				let sdata = {}
				console.log("2 weeks", response.data.filter(element=> (moment(element.timestamp) > moment().subtract(2, 'weeks'))).length)
				response.data.filter(element=> (moment(element.timestamp) > moment().subtract(2, 'weeks'))).map(element=>{return {...element, timestamp: moment(element.timestamp).startOf('day')}}).forEach(element => {
					console.log(sdata[moment(element.timestamp).format("MM-DD HH:mm")], element)
					if(!!sdata[moment(element.timestamp).format("MM-DD HH:mm")])
						sdata[moment(element.timestamp).format("MM-DD HH:mm")] += element.value
					else 
						sdata[moment(element.timestamp).format("MM-DD HH:mm")] = element.value
				});
				this.walkChartWeekly.data[0].data.push(...Object.keys(sdata).map(e=>sdata[e]))
				this.walkChartWeekly.labels.push(...Object.keys(sdata))
				sdata = {}
				response.data.map(element=>{return {...element, timestamp: moment(element.timestamp).startOf('week')}}).forEach(element => {
					if(!!sdata[moment(element.timestamp).format("MM-DD HH:mm")])
						sdata[moment(element.timestamp).format("MM-DD HH:mm")] += element.value
					else 
						sdata[moment(element.timestamp).format("MM-DD HH:mm")] = element.value
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
        console.log("resp", response)
				let sdata = {}
				response.data.filter(element=> (moment(element.timestamp) > moment().subtract(2, 'weeks'))).map(element=>{return {...element, timestamp: moment(element.timestamp).startOf('day')}}).forEach(element => {
					console.log(sdata[moment(element.timestamp).format("MM-DD HH:mm")], element)
					if(!!sdata[moment(element.timestamp).format("MM-DD HH:mm")])
						sdata[moment(element.timestamp).format("MM-DD HH:mm")] += element.value
					else 
						sdata[moment(element.timestamp).format("MM-DD HH:mm")] = element.value
				});
				this.walkChartWeekly.data[0].data.push(...Object.keys(sdata).map(e=>sdata[e]))
				this.walkChartWeekly.labels.push(...Object.keys(sdata))
				sdata = {}
				response.data.map(element=>{return {...element, timestamp: moment(element.timestamp).startOf('week')}}).forEach(element => {
					if(!!sdata[moment(element.timestamp).format("MM-DD HH:mm")])
						sdata[moment(element.timestamp).format("MM-DD HH:mm")] += element.value
					else 
						sdata[moment(element.timestamp).format("MM-DD HH:mm")] = element.value
				});
				this.walkChart.data[0].data.push(...Object.keys(sdata).map(e=>sdata[e]))
				this.walkChart.labels.push(...Object.keys(sdata))
				
      })
      .catch((err) => {
        console.log("err", err)
      })
		},
		calcHR() {
			let start_time = moment().subtract(2, 'weeks').format('YYYY-MM-DD HH:mm:ss.SSSS')
			let end_time = moment().format('YYYY-MM-DD HH:mm:ss.SSSS')
			console.log('https://api.personicle.org/data/read/datastreams?datatype=com.personicle.individual.datastreams.heartrate&startTime=' + start_time + '&endTime=' + end_time + '&source=google-fit')
			axios.get('https://api.personicle.org/data/read/datastreams?datatype=com.personicle.individual.datastreams.heartrate&startTime=' + start_time + '&endTime=' + end_time + '&source=google-fit',
				{
					headers: { Authorization: `Bearer ${this.token}` }
				})
				.then(response => {
					console.log("resp", response)
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
					console.log("walk", this.walkChart)
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
