<template>
  <div :id="id" :style="style"></div>
</template>

<script>
export default {
  name: 'charts',
  data () {
    return {
      chart: ''
    }
  },
  props: {
  	//这里子组件需要接收父组件传递过来的参数
  	id: {
  	  	type: String
  	},
  	width: {
  		type: String,
  		default: '100%'
  	},
  	height: {
  		type: String,
  		default: '100%'
  	},
  	option: {
  		type: Object,
  		//Object 类型的prop值需要用函数return出来，
  		//使用闭包保证一个vue实例拥有自己的一份props
  		default() {
  			return {
	  			title: {
	                text: 'ECharts 入门示例'
	            },
	            tooltip: {},
	            legend: {
	                data:['销量']
	            },
	            xAxis: {
			        type: 'category',
			        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
			    },
			    yAxis: {
			        type: 'value'
			    },
			    series: [{
			        data: [820, 932, 901, 934, 1290, 1330, 1320],
			        type: 'line'
			    }]
  			}
  		}
  	}
  },
  computed: {
  	style() {
  		return {
  			width: this.width,
  			height: this.height
  		}
  	}
  },
  watch: {
  	option: {
  		handler(newVal, oldVal) {
  			if (this.chart) {
  				this.chart.setOption(newVal)
  			} else {
  				this.init();
  			}
  		},
  		deep: true
  	}
  },
  mounted() {
  	this.init()
  },
  methods: {
  	init() {
  		this.chart = this.$echarts.init(document.getElementById(this.id))
  		this.chart.setOption(this.option)

  		window.addEventListener("resize", this.chart.resize);
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>