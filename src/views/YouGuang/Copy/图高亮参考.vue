<!DOCTYPE html>
<html lang="en"  style="height: 100%">
<head>
    <meta charset="UTF-8">
    <title>Map</title>
    <style>
        body{
            position: relative;
            background-color: #000000;
        }
        *{
             margin: 0;
             padding: 0;
             box-sizing: border-box;
         }
        ul,li{
            list-style: none;
        }
        .clear:after{
            display: block;
            content: "";
            clear:both;
        }

        #mainleft,#mainright{
            float:left;
            height: 85%;
            margin-top: -60px;
        }
        #mainleft{
            width:63%;
        }
        #mapchart{
            width: 100%;
            height: 100%;
        }

        /*悬浮框*/
        #plan{
            margin: 10px;
            background-color: #011C31;
            border-top: 1px solid #27BFC4;
            border-left: 1px solid #27BFC4;
            font-size: 12px;
            color: #fff;
            width: 200px;
        }
        #plan li{
            height: 20px;
            padding-left: 10px;
            border-bottom: 1px solid #27BFC4;

        }
        #plan li:first-child{
            font-size: 14px;
            height: 22px;
        }
        #plan li:first-child img{
            width: 10px;
            display: inline-block;
            margin:4px 4px 0 -4px;
        }
        #plan li span{
            display: inline-block;
        }
        #plan li span:first-child{
            width: 70px;
        }
        #plan li span:nth-child(2){
            width: 60px;
        }
        #plan li span:nth-child(3){
            width: 50px;
        }
        /*排行榜*/
        #mainright{
            width: 37%;
        }
        #mainright{
            padding: 10px;
        }
        #rank{
            background-color: rgba(119,119,119,.3);
            width:98%;
            height: 94%;
            color: white;
            position: relative;
        }
        #rank li p{
            float: left;
        }
        /*四个角*/
        #rank>li.corner>p{
            width: 16px;
            height: 16px;
        }
        #rank>li:first-child>p:first-child{
            float: left;
            border-top: 1px solid #27BFC4;
            border-left: 1px solid #27BFC4;
        }
        #rank>li:first-child>p:last-child{
            float: right;
            border-top: 1px solid #27BFC4;
            border-right: 1px solid #27BFC4;
        }
        #rank>li.corner:last-child{
            position: absolute;
            bottom:0;
            width: 100%;
        }
        #rank>li:last-child>p:first-child{
             float: left;
             border-bottom: 1px solid #27BFC4;
             border-left: 1px solid #27BFC4;
         }
        #rank>li:last-child>p:last-child{
            float: right;
            border-bottom: 1px solid #27BFC4;
            border-right: 1px solid #27BFC4;
        }
        /*排行榜主体*/
        #rank>li.thead{
            margin-bottom: 8px;
        }
        #rank>li.tobdy:hover{
            background-color: rgba(255,255,255,.2);
        }
        #rank>li.tobdy{
            height: 9.3%;
            padding-top: 10px;
        }
        #rank>li.tobdy>p:first-child{
            width: 20%;
        }
        #rank>li.tobdy>p:first-child span{
            display: block;
            width:20px;
            height: 20px;
            text-align: center;
            background-color: #27BFC4;
            margin:auto;
        }
        #rank>li.tobdy>p:nth-child(2){
            width: 25%;
        }

        /*进度条区域*/
        #rank>li.tobdy>div{
            float: left;
            width: 51%;
            height: 100%;
        }
        #rank>li.tobdy>div>ul li:first-child{
            float: left;
        }
        #rank>li.tobdy>div>ul li:last-child{
            float: right;
        }
        #rank p.prog-bg,#rank p.prog-on{
            height: 4px;
            border-radius:4px;
        }
        #rank p.prog-bg {
            width: 100%;
            margin-top: 4px;
            background-color: rgba(119,119,119,.5);
        }
        #rank p.prog-on{
            background-color: #95BA2E;
            margin-top: -4px;
        }
    </style>
    <script type="text/javascript" src="http://echarts.baidu.com/gallery/vendors/echarts/echarts.min.js"></script>
    <script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
    <script src="js/china.js"></script>
</head>
<body style="height: 100%; margin: 0;min-width: 1200px;min-height: 770px">

<div style="height: 10%;"></div>
<div id="mainleft">
    <div id="mapchart"></div>
</div>
<div id="mainright">
    <ul id="rank">
        <li class="corner clear">
            <p></p>
            <p></p>
        </li>
        <li class="thead clear">
            <p style="width: 20%;text-align: center">排行</p>
            <p style="width: 25%">地区</p>
            <p style="width: 40%">销量</p>
            <p style="width: 15%">完成率</p>
        </li>
        <li class="tobdy clear">
            <p>
                <span>1</span>
            </p>
            <p>江苏</p>
            <div class="prog">
                <ul class="clear">
                    <li>8920台</li>
                    <li>180%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 100%;"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>2</span></p>
            <p>浙江</p>
            <div class="prog">
                <ul class="clear">
                    <li>8588台</li>
                    <li>137%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 100%;"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>3</span></p>
            <p>四川</p>
            <div class="prog">
                <ul class="clear">
                    <li>8215台</li>
                    <li>110%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 100%;"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>4</span></p>
            <p>广东</p>
            <div class="prog">
                <ul class="clear">
                    <li>7586台</li>
                    <li>88%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 88%;"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>5</span></p>
            <p>山东</p>
            <div class="prog">
                <ul class="clear">
                    <li>6324台</li>
                    <li>78%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 78%;background-color: #1D9DCC"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>6</span></p>
            <p>福建</p>
            <div class="prog">
                <ul class="clear">
                    <li>6112台</li>
                    <li>72%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 72%;background-color: #1D9DCC"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>7</span></p>
            <p>湖南</p>
            <div class="prog">
                <ul class="clear">
                    <li>5989台</li>
                    <li>60%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 60%;background-color: #1D9DCC"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>8</span></p>
            <p>广西</p>
            <div class="prog">
                <ul class="clear">
                    <li>5448台</li>
                    <li>55%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 55%;background-color: #1D9DCC"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>9</span></p>
            <p>辽宁</p>
            <div class="prog">
                <ul class="clear">
                    <li>4994台</li>
                    <li>38%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 38%;background-color: #D36E52"></p>
            </div>
        </li>
        <li class="tobdy clear">
            <p><span>10</span></p>
            <p>江西</p>
            <div class="prog">
                <ul class="clear">
                    <li>4528台</li>
                    <li>22%</li>
                </ul>
                <p class="prog-bg"></p>
                <p class="prog-on" style="width: 22%;background-color: #D36E52"></p>
            </div>
        </li>
        <li class="corner clear">
            <p></p>
            <p></p>
        </li>
    </ul>
</div>

<script>
    //https://github.com/apache/incubator-echarts/tree/master/map
    //这个地址可以下载到地图文件
$(function () {
    var map = echarts.init(document.getElementById("mapchart"));
    var option = {

        tooltip: {
            trigger: "item",
            backgroundColor:'opacity',
            // alwaysShowContent:true,
            position: function (point, params, dom, rect, size) {

                $(dom).html(`
    <ul id="plan">
        <li><span><img src="img/local.png">${params.name}</span><span>完成率</span><span>销售量</span></li>
        <li><span>汽车</span><span>100%</span><span>2000台</span></li>
        <li><span>农用车</span><span>100%</span><span>2000台</span></li>
        <li><span>农业装备</span><span>100%</span><span>2000台</span></li>
        <li><span>环保装备</span><span>100%</span><span>2000台</span></li>
    </ul>
                `);
                // return ['2%', '70%'];//固定浮框的位置
            }
        },
        roamController: {
            x: "right",
            mapTypeControl: {
                china: true
            }
        },
        series:{
            name: "iphone3",
            type: "map",
            // roam:true,//支持鼠标缩放和移动
            zoom:1.2,//地图放大1.2倍
            mapType: "china",
            mapValueCalculation: "sum",
            label: {//图形上的文本标签,拥有label的一系列属性
                // show: true
            },
            emphasis: {//高亮状态下的样式
                label: {
                    show: true
                },
                itemStyle:{
                    areaColor:'#FEF200',
                    borderColor:'#D8B915',
                    borderWidth:2
                },
            },
            itemStyle: {
                // color: function (params) {
                //     var colorList = [
                //         '#C1232B', '#B5C334', '#FCCE10', '#E87C25', '#27727B',
                //         ......
                //     ];
                //     return colorList[params.dataIndex]
                // },
                color:function (params) {//seriesIndex, dataIndex, data, value
                    if(params.value<2000){
                        return '#65CAD4'
                    }else if(params.value>2000 && params.value<=4000){
                        return '#28BFC8'
                    }else if(params.value>4000 && params.value<=6000){
                        return '#24B4B5'
                    }else if(params.value>6000 && params.value<=8000){
                        return '#2E999F'
                    }else if(params.value>8000){
                        return '#25677F'
                    }
                }
            },
            data: [
                {
                    // value: [8920,123,456],//如果有更多数据可以这样存放，然后用params.data.value[i]获取
                    value: 8920,
                    name: "江苏",
                },
                {
                    value: 8588,
                    name: "浙江"
                },
                {
                    value: 8215,
                    name: "四川"
                },
                {
                    value: 7586,
                    name: "广东"
                },
                {
                    value: 6324,
                    name: "山东"
                },
                {
                    value: 6112,
                    name: "福建"
                },
                {
                    value: 5989,
                    name: "湖南"
                },
                {
                    value: 5448,
                    name: "广西"
                },
                {
                    value: 4994,
                    name: "辽宁"
                },
                {
                    value: 4528,
                    name: "江西"
                },
                {
                    value: 4767,
                    name: "安徽"
                },
                {
                    value: 4573,
                    name: "贵州"
                },
                {
                    value: 4544,
                    name: "湖北"
                },
                {
                    value: 3903,
                    name: "山西"
                },
                {
                    value: 3747,
                    name: "吉林"
                },
                {
                    value: 3342,
                    name: "黑龙江"
                },
                {
                    value: 3345,
                    name: "河南"
                },

                {
                    value: 2887,
                    name: "甘肃"
                },
                {
                    value: 2837,
                    name: "台湾"
                },
                {
                    value: 2673,
                    name: "内蒙古"
                },
                {
                    value: 2177,
                    name: "海南"
                },
                {
                    value: 2074,
                    name: "新疆"
                },
                {
                    value: 2783,
                    name: "河北"
                },
                {
                    value: 2354,
                    name: "上海"
                },
                {
                    value: 2093,
                    name: "北京"
                },
                {
                    value: 2034,
                    name: "重庆",
                },
                {
                    value: 1932,
                    name: "天津"
                },

                {
                    value: 1872,
                    name: "云南"
                },
                {
                    value: 1838,
                    name: "青海"
                },
                {
                    value: 1626,
                    name: "西藏"
                },
                {
                    value: 1563,
                    name: "陕西"
                },
                {
                    value: 1172,
                    name: "宁夏"
                },
                {
                    value: 677,
                    name: "香港"
                },
                {
                    value: 443,
                    name: "澳门"
                },
                {name: '南海诸岛',value: 0,
                    itemStyle:{
                        normal:{
                            opacity:0,
                            label:{show:false},
                            borderWidth:"0",borderColor:"#10242b",areaStyle:{color:'#10242b'}
                        }
                    }
                },
            ]
        }
    };

    map.setOption(option);

    map.dispatchAction({
        type:'showTip',//默认显示江苏的提示框
        seriesIndex: 0,//这行不能省
        dataIndex:0
    });

    $('li.tobdy').mouseenter(function () {
        var thisIndex = $(this).index()-2;//同辈的最前面还有两个li
        // $.each(data,function (i) {
        //     data[i].selected = false;
        // });
        // data[thisIndex].selected = true;
        // map.setOption(option);
        map.dispatchAction({
            type:'mapSelect',
            seriesIndex: 0,
            dataIndex:thisIndex
        });

        map.dispatchAction({
            type:'showTip',
            seriesIndex: 0,
            dataIndex:thisIndex
        });
    });

    $('li.tobdy').mouseleave(function () {
        var thisIndex = $(this).index()-2;
        // data[thisIndex].selected = false;
        // map.setOption(option);
        map.dispatchAction({
            type:'mapUnSelect',
            seriesIndex: 0,
            dataIndex:thisIndex
        });
        map.dispatchAction({
            type:'hideTip',
            seriesIndex: 0,
            dataIndex:thisIndex
        });
    });
    // map.on('click',function (params) {
    //     console.log(params.data.value);
    // });

    window.onresize = function () {
        map.resize();
    };
}());

</script>
</body>
</html>
