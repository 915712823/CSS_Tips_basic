<template>
  <div class="about">
     <el-carousel :interval="4000" type="card" height="200px">
        <el-carousel-item v-for="item in items" :key="item">
          <img :src="item" />
        </el-carousel-item>
      </el-carousel>

      <!-- 为 ECharts 准备一个具备大小（宽高）的 DOM -->
    <div ref="chart" style="width: 100%;height:400px;"></div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      items:[
        require('@/assets/img/1.png'),
        require('@/assets/img/2.png'),
        require('@/assets/img/3.png'),
        require('@/assets/img/4.png'),
        require('@/assets/img/5.png')
      ]
    }
  },
  mounted(){
    this.init()
  },
  methods:{
    init(){
      // 基于准备好的dom，初始化echarts实例
        var myChart = this.$echarts.init(this.$refs.chart);

        // 指定图表的配置项和数据
        var option =  {
    title: {
        text: '折线图堆叠'
    },
    tooltip: {
        trigger: 'axis'
    },
    legend: {
        data: ['邮件营销', '联盟广告', '视频广告', '直接访问', '搜索引擎']
    },
    grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
    },
    toolbox: {
        feature: {
            saveAsImage: {}
        }
    },
    xAxis: {
        type: 'category',
        boundaryGap: false,
        data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
    },
    yAxis: {
        type: 'value'
    },
    series: [
        {
            name: '邮件营销',
            type: 'line',
            stack: '总量',
            data: [120, 132, 101, 134, 90, 230, 210]
        },
        {
            name: '联盟广告',
            type: 'line',
            stack: '总量',
            data: [220, 182, 191, 234, 290, 330, 310]
        },
        {
            name: '视频广告',
            type: 'line',
            stack: '总量',
            data: [150, 232, 201, 154, 190, 330, 410]
        },
        {
            name: '直接访问',
            type: 'line',
            stack: '总量',
            data: [320, 332, 301, 334, 390, 330, 320]
        },
        {
            name: '搜索引擎',
            type: 'line',
            stack: '总量',
            data: [820, 932, 901, 934, 1290, 1330, 1320]
        }
    ]
};
        // 使用刚指定的配置项和数据显示图表。
        myChart.setOption(option);
    }
  }
}
</script>