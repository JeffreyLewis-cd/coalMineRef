<template>
    <div class="statisticDiagram">
        <div  class="statisticDiagram-title">
            <h2 class="head">
                <Icon type="compose"></Icon>
                <span>统计分析图表</span>
            </h2>
            <Button class="backToData" type="primary" @click="hideDiagram()">返回数据列表</Button>
        </div>

        <div class="subDiagramBtns">
        <ButtonGroup size="large">
            <Button class="subDiagramBtns-item" type="ghost"  v-for="(btnIntem,index) in btnIntems" :data-index="index"
                    :key="index" @click="subDiagram" :class="{'subDiagramBtns-item-active':btnIntem.active}">{{ btnIntem.name}}</Button>
        </ButtonGroup>
    </div>

        <div class="injuredAndDeath" >
            <div class="statisticDiagram-box" v-for="diagramitem in btnIntems"  :key="btnIntems.id"
                 v-show="diagramitem.active">
                <div class="statDiag-box-title">
                    <i class="icon-alibaba" :class="diagramitem.topicon"></i>
                    <p> {{diagramitem.name}} </p>
                </div>
                <div class="statDiag-box-item">
                    <Row>
                        <Col span="24">
                        <div class="diagram-innerBox diagram-container" >
                            <div :id="diagramitem.label" class="inner-box">
                            </div>
                        </div>
                        </Col>
                    </Row>
                </div>
            </div>
        </div>

        <div class="statistic-diagram-btn">
            <Button type="primary" @click="hideDiagram()">返回数据列表</Button>
        </div>
    </div>
</template>
<script>
    import chinaJson from './china.json'
    import HKJson from './xianggang.json'
    import {mapGetters} from 'vuex'
    import * as MUTATIONS from '../../../../store/mutations'
    import echarts from "echarts"

    export default{
        name:'statisticDiagram',
        data(){
            return{

            }
         },
        mounted: function () {
            this.initDiagram();            //创建diagram图表--进入页面初始化
        },
        methods:{
            hideDiagram: function () {
                this.$store.commit(MUTATIONS.diagramPageHide);  //切换统计图表页面
                this.$store.commit(MUTATIONS.hideStatisCondi);
            },
            subDiagram:function (e) {
                //active按钮样式；
                let subDiagramBtn=document.getElementsByClassName('subDiagramBtns-item');
                for(let key=0; key<subDiagramBtn.length; key++){
                    this.removeClass(subDiagramBtn[key],'subDiagramBtns-item-active');
                }
                this.addClass(e.target.parentNode,'subDiagramBtns-item-active');

                //active图表展示
                let activeIndex=e.currentTarget.dataset.index;
                console.log(activeIndex);
                this.$store.commit(MUTATIONS.activePage,activeIndex);

                //创建diagram图表
                this.creatDiagram(activeIndex);
            },

            //添加新的diagramBOX--清空旧的BOX;
            addNewDiagramBox:function (index) {
                //先去掉diagramBOX再添加相同的diagramBOX
                let diagramContainer=document.getElementsByClassName("diagram-container");
                for(let key=0; key<diagramContainer.length; key++){
                    document.getElementsByClassName("diagram-container")[key].innerHTML = ""; //先去掉
                }

                //创建diagram容器
                let oDiv = document.createElement('div');
                oDiv.id='diagramType'+index;
                oDiv.className="inner-box";
                document.getElementsByClassName('diagram-container')[index].appendChild(oDiv);

                //为diagramBOX添加样式
                let innerBox=document.getElementsByClassName('inner-box');
                for(let key=0; key<innerBox.length;key++){
                    innerBox[key].style.height="660px";
                    innerBox[key].style.width="1120px";
                    innerBox[key].style.padding="30px";
                    innerBox[key].style.border="1px solid #B6B6B6";
                    innerBox[key].style.borderRadius="5px";
                    innerBox[key].style.margin="10px";
                    innerBox[key].style.display="block";
                }
            },

            //添加新的diagramBOX--不清空;
            plusNewDiagram:function (index) {
                //创建diagram容器
                let oDiv = document.createElement('div');
                oDiv.id='diagramType'+index;
                oDiv.className="inner-box";
                document.getElementsByClassName('diagram-container')[0].appendChild(oDiv);

                //为diagramBOX添加样式
                let innerBox=document.getElementsByClassName('inner-box');
                for(let key=0; key<innerBox.length;key++){
                    innerBox[key].style.height="660px";
                    innerBox[key].style.width="1120px";
                    innerBox[key].style.padding="30px";
                    innerBox[key].style.border="1px solid #B6B6B6";
                    innerBox[key].style.borderRadius="5px";
                    innerBox[key].style.margin="10px";
                    innerBox[key].style.display="block";
                }
                console.log("plus111")
            },

            //柱状图0
            diagramBar0:function () {
                let diagramType0 = echarts.init(document.getElementById('diagramType0'));
                diagramType0.setOption({
                    title : {
                        text: '死亡人数统计',
                        subtext: '纯属虚构'
                    },
                    tooltip : {
                        trigger: 'axis'
                    },
                    legend: {
                        data:['2015年','2016年']
                    },
                    toolbox: {
                        show : true,
                        feature : {
                            dataView : {show: true, readOnly: false},
                            magicType : {show: true, type: ['line', 'bar']},
                            restore : {show: true},
                            saveAsImage : {show: true}
                        }
                    },
                    calculable : true,
                    xAxis : [
                        {
                            type : 'category',
                            data : ['1月','2月','3月','4月','5月','6月','7月','8月','9月','10月','11月','12月']
                        }
                    ],
                    yAxis : [
                        {
                            type : 'value'
                        }
                    ],
                    series : [
                        {
                            name:'2015年',
                            type:'bar',
                            data:[2.0, 4.9, 7.0, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20.0, 6.4, 3.3],
                            markPoint : {
                                data : [
                                    {type : 'max', name: '最大值'},
                                    {type : 'min', name: '最小值'}
                                ]
                            },
                            markLine : {
                                data : [
                                    {type : 'average', name: '平均值'}
                                ]
                            }
                        },
                        {
                            name:'2016年',
                            type:'bar',
                            data:[2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3],
                            markPoint : {
                                data : [
                                    {name : '年最高', value : 182.2, xAxis: 7, yAxis: 183},
                                    {name : '年最低', value : 2.3, xAxis: 11, yAxis: 3}
                                ]
                            },
                            markLine : {
                                data : [
                                    {type : 'average', name : '平均值'}
                                ]
                            }
                        }
                    ]
                });
            },
            //柱状图1
            diagramBar1:function () {
                let diagramType1 = echarts.init(document.getElementById('diagramType1'));
                diagramType1.setOption({
                    title: {
                        text: '受伤人数统计',
                        subtext: '数据来自网络'
                    },
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                            type: 'shadow'
                        }
                    },
                    legend: {
                        data: ['2015年', '2016年']
                    },
                    grid: {
                        left: '3%',
                        right: '4%',
                        bottom: '3%',
                        containLabel: true
                    },
                    xAxis: {
                        type: 'value',
                        boundaryGap: [0, 0.01]
                    },
                    yAxis: {
                        type: 'category',
                        data: ['第一季度','第二季度','第三季度','第四季度']
                    },
                    series: [
                        {
                            name: '2015年',
                            type: 'bar',
                            data: [203, 489, 290, 1049]
                        },
                        {
                            name: '2016年',
                            type: 'bar',
                            data: [195, 238, 310, 1214]
                        }
                    ]
                });
            },
            //柱状图2
            diagramBar2:function () {
                let diagramType2 = echarts.init(document.getElementById('diagramType2'));
                diagramType2.setOption({
                    tooltip : {
                        trigger: 'axis',
                        axisPointer : {            // 坐标轴指示器，坐标轴触发有效
                            type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
                        }
                    },
                    legend: {
                        data:['10万以下','10万~50万','50万~100万','100万-200万','200万~300万','300万~400万','400万~500万','500万~1000万','1000万以上']
                    },
                    grid: {
                        left: '3%',
                        right: '4%',
                        bottom: '3%',
                        containLabel: true
                    },
                    xAxis : [
                        {
                            type : 'category',
                            data : ['2010年','2011年','2012年','2013年','2014年','2015年','2016年']
                        }
                    ],
                    yAxis : [
                        {
                            type : 'value'
                        }
                    ],
                    series : [
                        {
                            name:'10万以下',
                            type:'bar',
                            data:[320, 332, 301, 334, 390, 330, 320]
                        },
                        {
                            name:'10万~50万',
                            type:'bar',
                            stack: '广告',
                            data:[120, 132, 101, 134, 90, 230, 210]
                        },
                        {
                            name:'50万~100万',
                            type:'bar',
                            stack: '广告',
                            data:[220, 182, 191, 234, 290, 330, 310]
                        },
                        {
                            name:'100万-200万',
                            type:'bar',
                            stack: '广告',
                            data:[150, 232, 201, 154, 190, 330, 410]
                        },
                        {
                            name:'200万~300万',
                            type:'bar',
                            data:[862, 1018, 964, 1026, 1679, 1600, 1570],
                            markLine : {
                                lineStyle: {
                                    normal: {
                                        type: 'dashed'
                                    }
                                },
                                data : [
                                    [{type : 'min'}, {type : 'max'}]
                                ]
                            }
                        },
                        {
                            name:'300万~400万',
                            type:'bar',
                            barWidth : 20,
                            stack: '搜索引擎',
                            data:[620, 732, 701, 734, 1090, 1130, 1120]
                        },
                        {
                            name:'400万~500万',
                            type:'bar',
                            stack: '搜索引擎',
                            data:[120, 132, 101, 134, 290, 230, 220]
                        },
                        {
                            name:'500万~1000万',
                            type:'bar',
                            stack: '搜索引擎',
                            data:[60, 72, 71, 74, 190, 130, 110]
                        },
                        {
                            name:'1000万以上',
                            type:'bar',
                            stack: '搜索引擎',
                            data:[62, 82, 91, 84, 109, 110, 120]
                        }
                    ]

                });
            },
            //柱状图3
            diagramBar3:function () {
                let diagramType3 = echarts.init(document.getElementById('diagramType3'));
                diagramType3.setOption({
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                            type: 'cross',
                            crossStyle: {
                                color: '#999'
                            }
                        }
                    },
                    toolbox: {
                        feature: {
                            dataView: {show: true, readOnly: false},
                            magicType: {show: true, type: ['line', 'bar']},
                            restore: {show: true},
                            saveAsImage: {show: true}
                        }
                    },
                    legend: {
                        data:['2015年','2016年','平均数']
                    },
                    xAxis: [
                        {
                            type: 'category',
                            data: ['1月','2月','3月','4月','5月','6月','7月','8月','9月','10月','11月','12月'],
                            axisPointer: {
                                type: 'shadow'
                            }
                        }
                    ],
                    yAxis: [
                        {
                            type: 'value',
                            name: '死亡人数',
                            min: 0,
                            max: 250,
                            interval: 50,
                            axisLabel: {
                                formatter: '{value} 人'
                            }
                        },
                        {
                            type: 'value',
                            name: '事故等级',
                            min: 0,
                            max: 25,
                            interval: 5,
                            axisLabel: {
                                formatter: '{value} 级'
                            }
                        }
                    ],
                    series: [
                        {
                            name:'2015年',
                            type:'bar',
                            data:[2.0, 4.9, 7.0, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20.0, 6.4, 3.3]
                        },
                        {
                            name:'2016年',
                            type:'bar',
                            data:[2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3]
                        },
                        {
                            name:'平均数',
                            type:'line',
                            yAxisIndex: 1,
                            data:[2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2]
                        }
                    ]
                });
            },

            //气泡图0
            diagramBubble0:function () {
                let dataYear = [
                    [[28604,77,17096869,'Australia',1990],[31163,77.4,27662440,'Canada',1990],[1516,68,115465773,'China',1990],[13670,74.7,10582082,'Cuba',1990],[28599,75,4986705,'Finland',1990],[29476,77.1,56943299,'France',1990],[31476,75.4,78958237,'Germany',1990],[28666,78.1,254830,'Iceland',1990],[1777,57.7,87061776,'India',1990]],
                    [[44056,81.8,23968973,'Australia',2015],[43294,81.7,35939927,'Canada',2015],[13334,76.9,137608943,'China',2015],[21291,78.5,11389562,'Cuba',2015],[38923,80.8,5503457,'Finland',2015],[37599,81.9,64395345,'France',2015],[44053,81.1,80688545,'Germany',2015],[42182,82.8,329425,'Iceland',2015],[5903,66.8,131150527,'India',2015]]
                ];
                let diagramType0 = echarts.init(document.getElementById('diagramType0'));
                diagramType0.setOption({
                    backgroundColor: new echarts.graphic.RadialGradient(0.6, 0.6, 0.8, [{
                        offset: 0,
                        color: '#f7f8fa'
                    }, {
                        offset: 1,
                        color: '#cdd0d5'
                    }]),
                    title: {
                        text: '1990 与 2015 年事故件数与财产损失'
                    },
                    legend: {
                        right: 10,
                        data: ['1990', '2015']
                    },
                    xAxis: {
                        splitLine: {
                            lineStyle: {
                                type: 'dashed'
                            }
                        }
                    },
                    yAxis: {
                        splitLine: {
                            lineStyle: {
                                type: 'dashed'
                            }
                        },
                        scale: true
                    },
                    series: [{
                        name: '1990',
                        data: dataYear[0],
                        type: 'scatter',
                        symbolSize: function (data) {
                            return Math.sqrt(data[2]) / 200;
                        },
                        label: {
                            emphasis: {
                                show: true,
                                formatter: function (param) {
                                    return param.data[3];
                                },
                                position: 'top'
                            }
                        },
                        itemStyle: {
                            normal: {
                                shadowBlur: 10,
                                shadowColor: 'rgba(120, 36, 50, 0.5)',
                                shadowOffsetY: 5,
                                color: new echarts.graphic.RadialGradient(0.4, 0.3, 1, [{
                                    offset: 0,
                                    color: 'rgb(251, 118, 123)'
                                }, {
                                    offset: 1,
                                    color: 'rgb(204, 46, 72)'
                                }])
                            }
                        }
                    }, {
                        name: '2015',
                        data: dataYear[1],
                        type: 'scatter',
                        symbolSize: function (data) {
                            return Math.sqrt(data[2]) / 200;
                        },
                        label: {
                            emphasis: {
                                show: true,
                                formatter: function (param) {
                                    return param.data[3];
                                },
                                position: 'top'
                            }
                        },
                        itemStyle: {
                            normal: {
                                shadowBlur: 10,
                                shadowColor: 'rgba(25, 100, 150, 0.5)',
                                shadowOffsetY: 5,
                                color: new echarts.graphic.RadialGradient(0.4, 0.3, 1, [{
                                    offset: 0,
                                    color: 'rgb(129, 227, 238)'
                                }, {
                                    offset: 1,
                                    color: 'rgb(25, 183, 207)'
                                }])
                            }
                        }
                    }]
                });
            },

            //气泡图1
            diagramBubble1:function () {
                let dataMonth = [
                    [[28604,77,17096869,'Australia','1月'],[31163,77.4,27662440,'Canada','1月'],[12516,68,115465773,'China','1月']],
                    [[44056,81.8,23968973,'Australia','2月'],[43294,81.7,35939927,'Canada','2月'],[13334,76.9,137608943,'China','2月']],
                    [[35056,71.8,2368973,'Australia','3月'],[34294,61.7,35919927,'Canada','3月'],[10334,56.9,13608943,'China','3月']],
                    [[2656,51.8,23918973,'Australia','4月'],[2394,51.7,35939127,'Canada','4月'],[1534,66.9,131608943,'China','4月']],
                ];
                let diagramType1 = echarts.init(document.getElementById('diagramType1'));
                diagramType1.setOption({
                    backgroundColor: new echarts.graphic.RadialGradient(0.6, 0.6, 0.8, [{
                        offset: 0,
                        color: '#f7f8fa'
                    }, {
                        offset: 1,
                        color: '#cdd0d5'
                    }]),
                    title: {
                        text: '1990 与 2015 年事故件数与财产损失'
                    },
                    legend: {
                        right: 10,
                        data: ['1月', '2月','3月','4月']
                    },
                    xAxis: {
                        splitLine: {
                            lineStyle: {
                                type: 'dashed'
                            }
                        }
                    },
                    yAxis: {
                        splitLine: {
                            lineStyle: {
                                type: 'dashed'
                            }
                        },
                        scale: true
                    },
                    series: [
                        {
                            name: '1月',
                            data: dataMonth[0],
                            type: 'scatter',
                            symbolSize: function (data) {
                                return Math.sqrt(data[2]) / 200;
                            },
                            label: {
                                emphasis: {
                                    show: true,
                                    formatter: function (param) {
                                        return param.data[3];
                                    },
                                    position: 'top'
                                }
                            },
                            itemStyle: {
                                normal: {
                                    shadowBlur: 10,
                                    shadowColor: 'rgba(120, 36, 50, 0.5)',
                                    shadowOffsetY: 5,
                                    color: new echarts.graphic.RadialGradient(0.4, 0.3, 1, [{
                                        offset: 0,
                                        color: 'rgb(251, 118, 123)'
                                    }, {
                                        offset: 1,
                                        color: 'rgb(204, 46, 72)'
                                    }])
                                }
                            }
                        },
                        {
                            name: '2月',
                            data: dataMonth[1],
                            type: 'scatter',
                            symbolSize: function (data) {
                                return Math.sqrt(data[2]) / 200;
                            },
                            label: {
                                emphasis: {
                                    show: true,
                                    formatter: function (param) {
                                        return param.data[3];
                                    },
                                    position: 'top'
                                }
                            },
                            itemStyle: {
                                normal: {
                                    shadowBlur: 10,
                                    shadowColor: 'rgba(25, 100, 150, 0.5)',
                                    shadowOffsetY: 5,
                                    color: new echarts.graphic.RadialGradient(0.4, 0.3, 1, [{
                                        offset: 0,
                                        color: 'rgb(129, 227, 238)'
                                    }, {
                                        offset: 1,
                                        color: 'rgb(25, 183, 207)'
                                    }])
                                }
                            }},
                        {
                            name: '3月',
                            data: dataMonth[2],
                            type: 'scatter',
                            symbolSize: function (data) {
                                return Math.sqrt(data[2]) / 200;
                            },
                            label: {
                                emphasis: {
                                    show: true,
                                    formatter: function (param) {
                                        return param.data[3];
                                    },
                                    position: 'top'
                                }
                            },
                            itemStyle: {
                                normal: {
                                    shadowBlur: 10,
                                    shadowColor: 'rgba(25, 100, 150, 0.5)',
                                    shadowOffsetY: 5,
                                    color: new echarts.graphic.RadialGradient(0.4, 0.3, 1, [{
                                        offset: 0,
                                        color: 'rgb(13, 20, 238)'
                                    }, {
                                        offset: 1,
                                        color: 'rgb(69, 50, 207)'
                                    }])
                                }
                            }
                        },
                        {
                            name: '4月',
                            data: dataMonth[3],
                            type: 'scatter',
                            symbolSize: function (data) {
                                return Math.sqrt(data[2]) / 200;
                            },
                            label: {
                                emphasis: {
                                    show: true,
                                    formatter: function (param) {
                                        return param.data[3];
                                    },
                                    position: 'top'
                                }
                            },
                            itemStyle: {
                                normal: {
                                    shadowBlur: 10,
                                    shadowColor: 'rgba(25, 100, 150, 0.5)',
                                    shadowOffsetY: 5,
                                    color: new echarts.graphic.RadialGradient(0.4, 0.3, 1, [{
                                        offset: 0,
                                        color: 'rgb(149, 227, 100)'
                                    }, {
                                        offset: 1,
                                        color: 'rgb(35, 183, 60)'
                                    }])
                                }
                            }
                        }
                    ]
                });

            },

            //瓦斯爆炸0
            gasExplosion0:function () {

                let echartDataLink="http://47.92.150.231:8080/cdis/statistics/result";

                //获取echart数据
                let echartData={};
                let postConfig= {
                    "AdvanceConditions": [
                        {
                            "TableName":"TB_CoalmineInfo",
                            "FieldName": "F_DesignedPC",
                            "FieldType": 2,
                            "FloatField":{
                                "IsRange":0,
                                "Operator":">=",
                                "Value":100
                            }
                        },
                        {
                            "TableName":"TB_CoalmineInfo",
                            "FieldName": "F_Enterprise_Property",
                            "FieldType": 4,
                            "DicField":{
                                "Values":["BF01-0102MK-QYXZ-01","BF01-0102MK-QYXZ-02"]
                            }
                        }
                    ]
                };

                this.axios.post(echartDataLink,postConfig)
                    .then((res)=> {
                        console.log(res);
                        echartData=res.data.Data;
                        for(let key3=0; key3<echartData.length; key3++){
                            let sEcharsType=echartData[key3].EchartsType;
                            if(sEcharsType=="1"){
                                let sEchartTitle=echartData[key3].Text;
                                let echatDataLegend=[];
                                let echartSeries=[];
                                let sEchartName=echartData[key3].Series.Name;
                                for(let key1=0; key1<echartData[key3].Legend.Data.length; key1++){
                                    echatDataLegend.push(echartData[key3].Legend.Data[key1])
                                }
                                for(let key2=0; key2<echartData[key3].Series.Data.length;key2++){
                                    let oSeries={
                                        value:echartData[key3].Series.Data[key2].Value,
                                        name:echartData[key3].Series.Data[key2].Name,
                                    };
                                    echartSeries.push(oSeries)
                                }

                                // 饼图01
                                let diagramType0 = echarts.init(document.getElementById('diagramType0'));
                                diagramType0.setOption({
                                    title : {
                                        text: sEchartTitle,
                                        subtext: '模拟数据',
                                        x:'center'
                                    },
                                    tooltip : {
                                        trigger: 'item',
                                        formatter: "{a} <br/>{b} : {c} ({d}%)"
                                    },

                                    legend: {
                                        orient: 'vertical',
                                        x: 'left',
                                        data:echatDataLegend
                                    },

                                    series : [
                                        {
                                            name: sEchartName,
                                            type: 'pie',
                                            radius : '55%',
                                            center: ['50%', '60%'],
                                            data:echartSeries,
                                            itemStyle: {
                                                emphasis: {
                                                    shadowBlur: 10,
                                                    shadowOffsetX: 0,
                                                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                                                }
                                            }
                                        }
                                    ]
                                });
                            }
                            else if(sEcharsType=="2"){
                                console.log('柱状图类型！');
                                let sEchartTitle=echartData[key3].Text;
                                let echatDataLegend=[];
                                let echartSeries=[];
                                let echartXAxis=[];
                                for(let key1=0; key1<echartData[key3].Legend.Data.length; key1++){
                                    echatDataLegend.push(echartData[key3].Legend.Data[key1])
                                }
                                for(let key5=0; key5<echartData[key3].XAxis.Data.length; key5++){
                                    echartXAxis.push(echartData[key3].XAxis.Data[key5])
                                }
                                for(let key4=0;key4<echartData[key3].Series.List.length;key4++){
                                    let echartDataItem={
                                        name:echartData[key3].Series.List[key4].Name,
                                        type:'bar',
                                        data:echartData[key3].Series.List[key4].Data,
                                    };
                                    echartSeries.push(echartDataItem);
                                }
                                console.log(echatDataLegend);
                                console.log(echartXAxis);
                                console.log(echartSeries);
                                // 柱状图01
                                let diagramType1 = echarts.init(document.getElementById('diagramType1'));
                                diagramType1.setOption({
                                    title : {
                                        text: sEchartTitle,
                                    },
                                    tooltip: {
                                        trigger: 'axis',
                                        axisPointer: {
                                            type: 'cross',
                                            crossStyle: {
                                                color: '#999'
                                            }
                                        }
                                    },
                                    toolbox: {
                                        feature: {
                                            dataView: {show: true, readOnly: false},
                                            magicType: {show: true, type: ['line', 'bar']},
                                            restore: {show: true},
                                            saveAsImage: {show: true}
                                        }
                                    },
                                    legend: {
                                        data:echatDataLegend
                                    },
                                    xAxis: [
                                        {
                                            type: 'category',
                                            data: echartXAxis,
                                            axisPointer: {
                                                type: 'shadow'
                                            }
                                        }
                                    ],
                                    yAxis : [
                                        {
                                            type : 'value'
                                        }
                                    ],
                                    series: echartSeries
                                });
                            }
                        }
                    })
                    .catch(function (error) {
                        // 处理失败的结果
                        console.log(error);
                        console.log('更多条件-请求失败-get！')
                    });
            },

            //瓦斯中毒1
            gasPoision1:function () {
                let diagramType1 = echarts.init(document.getElementById('diagramType1'));
                diagramType1.setOption({
                    title : {
                        text: '中毒事故地点瓦斯浓度',
                        subtext: '模拟数据',
                        x:'center'
                    },
                    tooltip : {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c} ({d}%)"
                    },
                    legend: {
                        orient: 'vertical',
                        x: 'left',
                        data:['瓦斯浓度5％～10％','瓦斯浓度10％～15％','瓦斯浓度15％～20％','瓦斯浓度20％～25％','瓦斯浓度25％～30％',
                            '瓦斯浓度30％～35％','瓦斯浓度35％～40％','瓦斯浓度40％～45％']
                    },

                    series : [
                        {
                            name: '访问来源',
                            type: 'pie',
                            radius : '55%',
                            center: ['50%', '60%'],
                            data:[
                                {value:624, name:'瓦斯浓度5％～10％'},
                                {value:310, name:'瓦斯浓度10％～15％'},
                                {value:234, name:'瓦斯浓度15％～20％'},
                                {value:23, name:'瓦斯浓度20％～25％'},
                                {value:312, name:'瓦斯浓度25％～30％'},
                                {value:156, name:'瓦斯浓度30％～35％'},
                                {value:513, name:'瓦斯浓度35％～40％'},
                                {value:12, name:'瓦斯浓度40％～45％'}
                            ],
                            itemStyle: {
                                emphasis: {
                                    shadowBlur: 10,
                                    shadowOffsetX: 0,
                                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                                }
                            }
                        }
                    ]
                });
            },

            //瓦斯突出2
            gasOutput2:function () {
                let diagramType2 = echarts.init(document.getElementById('diagramType2'));
                // 饼图03
                diagramType2.setOption({
                    title : {
                        text: '突出类型',
                        subtext: '模拟数据',
                        x:'center'
                    },
                    tooltip : {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c} ({d}%)"
                    },
                    legend: {
                        orient: 'vertical',
                        x: 'left',
                        data:['突出，在地压和瓦斯联合作用下产生','压出，主要由地压造成','倾出，煤岩倾出后']
                    },

                    series : [
                        {
                            name: '访问来源',
                            type: 'pie',
                            radius : '55%',
                            center: ['50%', '60%'],
                            data:[
                                {value:624, name:'突出，在地压和瓦斯联合作用下产生'},
                                {value:310, name:'压出，主要由地压造成'},
                                {value:168, name:'倾出，煤岩倾出后'}
                            ],
                            itemStyle: {
                                emphasis: {
                                    shadowBlur: 10,
                                    shadowOffsetX: 0,
                                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                                }
                            }
                        }
                    ]
                });
            },

            //水源0
            waterSource0:function () {
                let diagramType0 = echarts.init(document.getElementById('diagramType0'));
                // 饼图01
                diagramType0.setOption({
                    title : {
                        text: '水源',
                        subtext: '模拟数据',
                        x:'center'
                    },
                    tooltip : {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c} ({d}%)"
                    },

                    legend: {
                        orient: 'vertical',
                        x: 'left',
                        data:['地下水','管道漏水','山区洪水','地下河流','溶洞蓄水']
                    },

                    series : [
                        {
                            name: '访问来源',
                            type: 'pie',
                            radius : '55%',
                            center: ['50%', '60%'],
                            data:[
                                {value:61, name:'地下水'},
                                {value:98, name:'管道漏水'},
                                {value:102, name:'山区洪水'},
                                {value:135, name:'地下河流'},
                                {value:382, name:'溶洞蓄水'}
                            ],
                            itemStyle: {
                                emphasis: {
                                    shadowBlur: 10,
                                    shadowOffsetX: 0,
                                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                                }
                            }
                        }
                    ]
                });
            },

            //突水通道1
            waterTunnel1:function () {
                let diagramType1 = echarts.init(document.getElementById('diagramType1'));
                //柱状图01
                diagramType1.setOption({
                    title : {
                        text: '突水通道',
                        subtext: '纯属虚构'
                    },
                    tooltip : {
                        trigger: 'axis'
                    },
                    legend: {
                        data:['2015年','2016年']
                    },
                    toolbox: {
                        show : true,
                        feature : {
                            dataView : {show: true, readOnly: false},
                            magicType : {show: true, type: ['line', 'bar']},
                            restore : {show: true},
                            saveAsImage : {show: true}
                        }
                    },
                    calculable : true,
                    xAxis : [
                        {
                            type : 'category',
                            data : ['1月','2月','3月','4月','5月','6月','7月','8月','9月','10月','11月','12月']
                        }
                    ],
                    yAxis : [
                        {
                            type : 'value'
                        }
                    ],
                    series : [
                        {
                            name:'2015年',
                            type:'bar',
                            data:[2.0, 4.9, 7.0, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20.0, 6.4, 3.3],
                            markPoint : {
                                data : [
                                    {type : 'max', name: '最大值'},
                                    {type : 'min', name: '最小值'}
                                ]
                            },
                            markLine : {
                                data : [
                                    {type : 'average', name: '平均值'}
                                ]
                            }
                        },
                        {
                            name:'2016年',
                            type:'bar',
                            data:[2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3],
                            markPoint : {
                                data : [
                                    {name : '年最高', value : 182.2, xAxis: 7, yAxis: 183},
                                    {name : '年最低', value : 2.3, xAxis: 11, yAxis: 3}
                                ]
                            },
                            markLine : {
                                data : [
                                    {type : 'average', name : '平均值'}
                                ]
                            }
                        }
                    ]
                });
            },

            //水量2
            waterVolume2:function () {
                let diagramType2 = echarts.init(document.getElementById('diagramType2'));
                // 绘制图表
                diagramType2.setOption({
                    title: {
                        text: '水量',
                        subtext: '模拟数据',
                        x:'left'
                    },
                    tooltip : {
                        trigger: 'axis',
                        axisPointer: {
                            type: 'cross',
                            label: {
                                backgroundColor: '#6a7985'
                            }
                        }
                    },
                    legend: {
                        x:'right',
                        data:['1000方以下','1000方~2000方','2000方~3000方','3000方~4000方','4000方~5000方']
                    },
                    toolbox: {
                        feature: {
                            saveAsImage: {}
                        }
                    },
                    grid: {
                        left: '3%',
                        right: '4%',
                        bottom: '3%',
                        containLabel: true
                    },
                    xAxis : [
                        {
                            type : 'category',
                            boundaryGap : false,
                            data : ['2010','2011','2012','2013','2014','2015','2016']
                        }
                    ],
                    yAxis : [
                        {
                            type : 'value'
                        }
                    ],
                    series : [
                        {
                            name:'1000方以下',
                            type:'line',
                            stack: '总量',
                            areaStyle: {normal: {}},
                            data:[120, 132, 101, 134, 90, 230, 210]
                        },
                        {
                            name:'1000方~2000方',
                            type:'line',
                            stack: '总量',
                            areaStyle: {normal: {}},
                            data:[220, 182, 191, 234, 290, 330, 310]
                        },
                        {
                            name:'2000方~3000方',
                            type:'line',
                            stack: '总量',
                            areaStyle: {normal: {}},
                            data:[150, 232, 201, 154, 190, 330, 410]
                        },
                        {
                            name:'3000方~4000方',
                            type:'line',
                            stack: '总量',
                            areaStyle: {normal: {}},
                            data:[320, 332, 301, 334, 390, 330, 320]
                        },
                        {
                            name:'4000方~5000方',
                            type:'line',
                            stack: '总量',
                            label: {
                                normal: {
                                    show: true,
                                    position: 'top'
                                }
                            },
                            areaStyle: {normal: {}},
                            data:[820, 932, 901, 934, 1290, 1330, 1320]
                        }
                    ]
                });
            },

            //创建diagram图表--需要点击小按钮
            creatDiagram:function (activeIndex) {
                if(this.btnindex=='1'){
                    switch (activeIndex){
                        case '0':
                            console.log(activeIndex);
                            this.addNewDiagramBox(activeIndex);
                            this.diagramBar0();                //柱状图0
                            break;
                        case '1':
                            console.log(activeIndex);
                            this.addNewDiagramBox(activeIndex);
                            this.diagramBar1();                 //柱状图1
                            break;
                        case '2':
                            console.log('柱3');
                            this.addNewDiagramBox(activeIndex);
                            this.diagramBar2();                 //柱状图2
                            break;
                        case '3':
                            console.log('柱4');
                            this.addNewDiagramBox(activeIndex);
                            this.diagramBar3();                 //柱状图3
                            break;
                    }
                }
                else if(this.btnindex=='2'){
                    switch (activeIndex){
                        case '0':
                            this.addNewDiagramBox(activeIndex);
                            this.diagramBubble0();    //气泡图0
                            break;
                        case '1':
                            this.addNewDiagramBox(activeIndex);
                            this.diagramBubble1();    //气泡图1
                            break;
                    }
                }
                else if(this.btnindex=='7'){
                    switch (activeIndex) {
                        case '0':
                            // 添加新的diagramBOX
                            this.addNewDiagramBox(activeIndex);
                            this.plusNewDiagram("1");
                            this.gasExplosion0();      //瓦斯爆炸0
                            break;
                        case '1':
                            this.addNewDiagramBox(activeIndex);
                            this.gasPoision1();       //瓦斯中毒1
                            break;
                        case '2':
                            this.addNewDiagramBox(activeIndex);
                            this.gasOutput2();         //瓦斯突出2
                            break;
                    }

                }
                else if(this.btnindex=='8'){
                    switch (activeIndex){
                        case '0':
                            this.addNewDiagramBox(activeIndex);
                            this.waterSource0();        //水源0
                            break;
                        case '1':
                            this.addNewDiagramBox(activeIndex);
                            this.waterTunnel1();        //突水通道1
                            break;
                        case '2':
                            this.addNewDiagramBox(activeIndex);
                            this.waterVolume2();        //水量2
                            break;
                    }
                }
            },

            //创建diagram图表--进入页面初始化
            initDiagram:function () {
                if(this.btnindex=='1'){
                    console.log('初始化1');
                    this.addNewDiagramBox("0");
                    this.diagramBar0();                //柱状图0
                }
                else if(this.btnindex=='2'){
                    console.log('初始化2');
                    this.addNewDiagramBox("0");
                    this.diagramBubble0();    //气泡图0
                }
                else if(this.btnindex=='7'){
                    console.log('初始化7');
                    this.addNewDiagramBox("0");
                    this.plusNewDiagram("1");
                    this.gasExplosion0();      //瓦斯爆炸0
                }
                else if(this.btnindex=='8'){
                    console.log('初始化8');
                    this.addNewDiagramBox("0");
                    this.waterSource0();      //水源0
                }

            },

            addClass:function(obj, cls){
                let obj_class = obj.className,//获取 class 内容.
                    blank = (obj_class != '') ? ' ' : '';//判断获取到的 class 是否为空, 如果不为空在前面加个'空格'.
                let added = obj_class + blank + cls;//组合原来的 class 和需要添加的 class.
                obj.className = added;//替换原来的 class.
            },
            removeClass:function (obj, cls){
                let obj_class = ' '+obj.className+' ';//获取 class 内容, 并在首尾各加一个空格. ex) 'abc    bcd' -> ' abc    bcd '
                obj_class = obj_class.replace(/(\s+)/gi, ' ');//将多余的空字符替换成一个空格. ex) ' abc    bcd ' -> ' abc bcd '
                let removed = obj_class.replace(' '+cls+' ', ' ');//在原来的 class 替换掉首尾加了空格的 class. ex) ' abc bcd ' -> 'bcd '
                removed = removed.replace(/(^\s+)|(\s+$)/g, '');//去掉首尾空格. ex) 'bcd ' -> 'bcd'
                obj.className = removed;//替换原来的 class.
            },
            
        },
        computed:{
                ...mapGetters({
                    staticDiagram:'staticDiagram',
                    statisDiagramPage:'statisDiagramPage',
                    gasDiagrams:'gasDiagrams',
                    injuredAndDeathDiagrams:'injuredAndDeathDiagrams',
                    btnIntems:'btnIntems',
                    btnindex:'btnindex'
                })
        }
    }

</script>

<style scoped>
    .statisticDiagram{
        width:1166px;
        margin:0 auto;
        padding:30px 0;

    }
    .statisticDiagram-box{
        width:1166px;
        background: #ffffff;
        border:1px solid #B6B6B6;
        border-radius: 5px;
        padding:10px;
        margin-bottom:15px;
    }
    .statisticDiagram-title{
        height:50px;
        line-height:50px;
    }
    .statisticDiagram-title .backToData{
        float: right;
    }
    .statisticDiagram-title .head{
        float: left;
    }
    .inner-box{
        height:660px;
        width:1120px;
        padding:30px;
        border:1px solid #B6B6B6;
        border-radius: 5px;
        margin:10px;
        display: block;
    }

    .statDiag-box-title{
        margin-left: 10px;
        font-size: 16px;
        font-weight: bold;
        height:40px;
        line-height:40px;
    }
    .statDiag-box-title .statDiag-explosion{
        background: url("../../../../assets/pic/icons/images/explosive01.png") no-repeat;
        background-size: cover;
    }
    .statDiag-box-title .statDiag-poision{
        background: url("../../../../assets/pic/icons/images/poision02.png") no-repeat;
        background-size: cover;
    }
    .statDiag-gasOutput{
        background: url("../../../../assets/pic/icons/images/gasOutput01.png") no-repeat;
        background-size: cover;
    }
    .statDiag-historyTrend{
        background: url("../../../../assets/pic/icons/images/trend02.png") no-repeat;
        background-size: cover;
    }
    .statDiag-injured01{
        background: url("../../../../assets/pic/icons/images/injured01.png") no-repeat;
        background-size: cover;
    }
    .statDiag-level01{
        background: url("../../../../assets/pic/icons/images/level01.png") no-repeat;
        background-size: cover;
    }
    .statDiag-money01{
        background: url("../../../../assets/pic/icons/images/money01.png") no-repeat;
        background-size: cover;
    }
    .statDiag-death01{
        background: url("../../../../assets/pic/icons/images/death01.png") no-repeat;
        background-size: cover;
    }
    .statDiag-incidentsArea{
        background: url("../../../../assets/pic/icons/images/map03.png") no-repeat;
        background-size: cover;
    }
    .statDiag-waterSource1{
        background: url("../../../../assets/pic/icons/images/waterSource1.png") no-repeat;
        background-size: cover;
    }
    .statDiag-waterTunnel1{
        background: url("../../../../assets/pic/icons/images/waterTunnel1.png") no-repeat;
        background-size: cover;
    }
    .statDiag-waterVolume1{
        background: url("../../../../assets/pic/icons/images/waterVolume1.png") no-repeat;
        background-size: cover;
    }
    .statDiag-box-title p{
        height:30px;
        width:200px;
        line-height:30px;
        float: left;
        margin-top: 5px;
        margin-left: 5px;
    }
    .diagram-innerBox{
        float: left;
    }

    .statistic-diagram-btn{
        width:1166px;
        height:30px;
        line-height:30px;
        text-align: right;
        margin:20px auto
    }
    .subDiagramBtns{
        margin:10px 0;
    }
    .subDiagramBtns-item{
        background: #ffffff;
    }
    .subDiagramBtns-item-active{
        background: #2D8CF0;
        color: #ffffff;
    }

</style>
