<template />

<script>
export default {
  name: 'ShortVisit',
  data() {
  },
  methods: {
    drawLine() {
      this.GetRandom(this.list1)
      var myChart = echarts.init(document.getElementById('relate_graph3'))
      var option = {
        // backgroundColor: new echarts.graphic.RadialGradient(0.3, 0.3, 0.8, [{
        //     offset: 0,
        //     color: '#fff'
        // }, {
        //     offset: 1,
        //     color: '#cdd0d5'
        // }]),
        animationDurationUpdate: 1500,
        animationEasingUpdate: 'quinticInOut',
        series: [{
          type: 'graph',
          layout: 'none',
          legendHoverLink: true, // 是否启用图例 hover(悬停) 时的联动高亮。
          hoverAnimation: true, // 是否开启鼠标悬停节点的显示动画
          data: this.list1.map(function(node) {
            return {
              x: node.x,
              y: node.y,
              id: node.id,
              symbolSize: node.psize,
              symbolSize1: node.csize,
              name: node.name,
              itemStyle: {
                normal: {
                  label: {
                    show: true
                  },
                  color: node.color,
                  opacity: 1
                },
                emphasis: {
                  label: {
                    show: true
                  },
                  color: node.color,
                  opacity: 1
                }
              }
            }
          }),
          edges: this.list2.map(function(edge) {
            return {
              source: edge.sourceId,
              target: edge.targetId
            }
          }),
          label: { // =============图形上的文本标签
            normal: {
              show: true, // 是否显示标签。
              position: 'outside', // 标签的位置。['50%', '50%'] [x,y]
              textStyle: { // 标签的字体样式
                fontStyle: 'normal', // 文字字体的风格 'normal'标准 'italic'斜体 'oblique' 倾斜
                fontWeight: 'bolder', // 'normal'标准'bold'粗的'bolder'更粗的'lighter'更细的或100 | 200
                fontFamily: 'sans-serif', // 文字的字体系列
                fontSize: 12 // 字体大小
              }
            },
            emphasis: { // 高亮状态
              show: true,
              textStyle: { // 标签的字体样式
                fontStyle: 'normal', // 文字字体的风格 'normal'标准 'italic'斜体 'oblique' 倾斜
                fontWeight: 'bolder', // 'normal'标准'bold'粗的'bolder'更粗的'lighter'更细的或100 | 200
                fontFamily: 'sans-serif', // 文字的字体系列
                fontSize: 12 // 字体大小
              }
            }
          },
          edgeSymbol: ['arrow', 'none'],
          roam: true,
          focusNodeAdjacency: true, // 是否在鼠标移到节点上的时候突出显示节点以及节点的边和邻接节点
          lineStyle: { // ==========关系边的公用线条样式。
            normal: {
              color: '#909399',
              width: '1',
              type: 'solid', // 线的类型 'solid'（实线）'dashed'（虚线）'dotted'（点线）
              curveness: 0.3, // 线条的曲线程度，从0到1
              opacity: 0.6
              // 图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。默认0.5
            },
            emphasis: { // 高亮状态
              width: '2',
              color: '#909399',
              type: 'solid', // 线的类型 'solid'（实线）'dashed'（虚线）'dotted'（点线）
              curveness: 0.3, // 线条的曲线程度，从0到1
              opacity: 1
            }
          },
          edgeLabel: { // ==============线条的边缘标签
            normal: {
              show: false,
              textStyle: {
                fontSize: 10
              }
            },
            emphasis: { // 高亮状态
              show: false,
              textStyle: {
                fontSize: 12
              }
            }
          }
        }],
        // toolbox: { //==============可以保存为图片
        //     show: true,
        //     feature: {
        //         dataView: {
        //             show: true,
        //             readOnly: true
        //         },
        //         restore: {
        //             show: true
        //         },
        //         saveAsImage: {
        //             show: true
        //         }
        //     }
        // },
        tooltip: { // ==============显示鼠标移入的显示
          triggerOn: 'click', // 点击  mousemove
          enterable: true,
          hideDelay: 50,
          padding: 0,
          confine: true,
          formatter: function(params, ticket, callback) {
            if (params.dataType === 'node') {
              var html = ''
              html += '<div class="dialogShowR" v-scrollBar>'
              html += '<div>服务名称：租赁保证金</div>'
              html += '<div>协议类型：http</div>'
              html += '<div>监听端口号：8089</div>'
              html += '<div>服务审批状态：发布-待审核</div>'
              html += '<div>服务版本号：1.1</div>'
              html += '<div>服务接口数：43</div>'
              html += '<div>最后编辑时间：2018-10-11 12:00:00</div>'
              html += '<div class="desc">简要描述：<p>针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存</p></div>'
              html += '<div class="desc">服务描述：<p>针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对针对境外的存款人员的业务针对</p></div>'
              html += '<div>被依赖的服务数量为：' + params.data.symbolSize1 + '</div>'
              html += '<div>被依赖的服务数量为：' + params.data.symbolSize + '</div>'
              html += '</div>'
              return html
            } else if (params.dataType === 'edge') {
              var html1 = ''
              html1 += '<div class="dialogShow"><h5>服务源代码为：' + params.data.source + '</h5></div>'
              return html1
            }
          }
        }
      }
      myChart.setOption(option) // 设置图属性
      myChart.on('mouseover', function(params) {
        if (params.dataType === 'node') {
          const options = myChart.getOption()
          const nodesOption = options.series[0].data
          const linksOption = options.series[0].edges
          for (const m in nodesOption) { // m是每个节点
            const arr = []
            for (const i in linksOption) { // 遍历边
              arr.push(linksOption[i].target) // 加入尾节点
            }
            if (nodesOption[m].name === params.name) { // 看不懂？？？？？？？？？？？？？？？
              nodesOption[m].itemStyle.opacity = 1
              for (const j in linksOption) { // j是每条边
                if (linksOption[j].source == params.data.id) { // ??????????
                  options.series[0].lineStyle.opacity = 1
                }
              }
            } else if (arr.indexOf(nodesOption[m].id)) {
              nodesOption[m].itemStyle.opacity = 1 // 出现过的数据
            } else {
              nodesOption[m].itemStyle.opacity = 0.1 // 不要的数据
            }
          }
          myChart.setOption(options)
        }
        myChart.dispatchAction({
          type: 'focusNodeAdjacency',
          dataIndex: params.dataIndex // dataIndex??????????????????
        })
      })
      myChart.on('mouseout', function(params) {
        myChart.dispatchAction({
          type: 'unfocusNodeAdjacency',
          seriesIndex: 0
        })
      })
      // ------------------------------------------------------------以上是高亮部分
      // this.$refs.myCharts.oncontextmenu = () => false;
      myChart.on('contextmenu', function(param) {
        document.oncontextmenu = () => false
        const menu = document.getElementById('menuuu')
        const event = param.event
        const pageX = event.offsetX
        const pageY = event.offsetY
        console.log(pageX, 'pageX')
        menu.style.left = (pageX + 40) + 'px'// 右键出菜单部分
        menu.style.top = (pageY + 60) + 'px'// 右键出菜单部分
        menu.style.display = 'block'
      })
    },
    GetRandom(list) {
      for (var i = 0; i < this.list1.length; i++) {
        var x = Math.floor(Math.random() * 100)
        var y = Math.floor(Math.random() * 100)
        var colorAll = ['#a75ebc', '#ff7e00', '#f6e0ff', '#ff0000']
        var n = Math.floor(Math.random() * 5)
        var color = colorAll[n]
        this.list1[i].x = x
        this.list1[i].y = y
        this.list1[i].color = color
      }
    },
    handleSearch() {
      var myChart1 = echarts.init(document.getElementById('relate_graph3'))
      const options = myChart1.getOption()
      const nodesOption = options.series[0].data
      const linksOption = options.series[0].edges
      for (const m in nodesOption) {
        nodesOption[m].itemStyle.opacity = 1
        if (nodesOption[m].name.indexOf(this.input) > -1) { // 先比较节点是否在
          for (const k in linksOption) {
            if (linksOption[k].source == nodesOption[m].id) { // 同时还显示其相邻边???????????????????????????????????????
              options.series[0].lineStyle.opacity = 1 // 通过修改该节点的透明度来实现高亮的效果
            }
          }
        } else {
          nodesOption[m].itemStyle.opacity = 0.1
        }
        options.series[0].lineStyle.opacity = 0.1
      }
      myChart1.setOption(options)
    },
    handleRadio() {
      const myChart1 = echarts.init(document.getElementById('relate_graph3'))
      const options = myChart1.getOption()
      if (this.radio1 === '1') {
        options.series[0].label.show = true// 控制是否显示label
      } else {
        options.series[0].label.show = false// 控制是否显示label
      }
      // console.log(options, 'options');
      myChart1.setOption(options)
    },
    handleRadio1() {
      const myChart1 = echarts.init(document.getElementById('relate_graph3'))
      const options = myChart1.getOption()
      const myIMG = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQsAAAFyCAYAAADieP9bAAAAAXNSR0IArs4c6QAAAAlwSFlzAAAXEgAAFxIBZ5/SUgAAQABJREFUeAHsvQlwHOl15/kyswr3DQIgTgK8bz'
      if (this.radio === '1') {
        // options.series[0].symbol = "image://http://thumb12.jfcdns.com/2018-06/bce5b231ad7df722.png"; //修改节点样式为图片样式
        options.series[0].symbol = `image://${myIMG}` // 修改节点样式为图片样式
      } else {
        options.series[0].symbol = 'circle'// 修改图片样式为节点样式
        // console.log(options, 'options');
      }
      myChart1.setOption(options)
    }

  }
}
</script>

<style rel="stylesheet/scss" lang="scss">

</style>
