<template>
    <div>
        <div class="accidentsDetails">
            <div class="accidentsDetails-title">
                <Icon type="clipboard"></Icon>
                <span>数据详情</span>
            </div>

            <div class="accidentsDetails-table">
                <Row class="for-border-left">
                    <Col span="4" class="table-td "> <span> 事故类型 </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.claVal}} </span> </Col>
                    <Col span="4" class="table-td"> <span> 事故级别 </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.levelVal}} </span> </Col>
                    <Col span="4" class="table-td"> <span> 事故时间 </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.dateVal}} </span> </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td"> <span> 事故地点 </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.addressVal}} </span> </Col>
                    <Col span="4" class="table-td"> <span> 巷道类型 </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.tunnelVal}} </span> </Col>
                    <Col span="4" class="table-td"> <span> 支护方式 </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.supportVal}} </span> </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td"> <span> 标高（m） </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.standHVal}} </span> </Col>
                    <Col span="4" class="table-td"> <span> 埋深(m) </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.buriDepVal}} </span> </Col>
                    <Col span="4" class="table-td"> <span> 作用情况 </span> </Col>
                    <Col span="4" class="table-td"> <span> {{tableData.operationVal}} </span> </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td table-td-3"> <span> 煤层特征 </span> </Col>
                    <Col span="4" class="table-td table-td-3">
                        <p class="table-td-inner">名称</p>
                        <p class="table-td-inner">倾角</p>
                        <p class=" table-td-borderNone">厚度</p>
                    </Col>
                    <Col span="4" class="table-td table-td-3">
                        <p class="table-td-inner">{{tableData.coalFname}}</p>
                        <p class="table-td-inner">{{tableData.coalAngle}}</p>
                        <p class=" table-td-borderNone">{{tableData.coalthickness}}</p>
                    </Col>
                    <Col span="4" class="table-td table-td-3">
                        <p class="table-td-inner">硬度</p>
                        <p class="table-td-inner">上邻近层</p>
                        <p class=" table-td-borderNone">下邻近层</p>
                    </Col>
                    <Col span="8" class="table-td table-td-3">
                        <p class="table-td-inner">{{tableData.hardness}}</p>
                        <p class="table-td-inner">{{tableData.upperFormation}}</p>
                        <p class=" table-td-borderNone">{{tableData.lowerForation}}</p>
                    </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td"> <span> 地质构造 </span> </Col>
                    <Col span="20" class="table-td"> <span> {{tableData.geoStructure}} </span> </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td table-td-4"> <span> 通风情况 </span> </Col>
                    <Col span="4" class="table-td table-td-4">
                        <p class="table-td-inner">正常瓦斯浓度（%）</p>
                        <p class="table-td-inner">最高瓦斯浓度（%）</p>
                        <p class="table-td-inner">有效风量（m3/min）</p>
                        <p class=" table-td-borderNone">绝对瓦斯量（m3/min）</p>
                    </Col>
                    <Col span="4" class="table-td table-td-4">
                        <p class="table-td-inner">{{tableData.gasConcentration}}</p>
                        <p class="table-td-inner">{{tableData.maxConcentration}}</p>
                        <p class="table-td-inner">{{tableData.airVolume}}</p>
                        <p class=" table-td-borderNone">{{tableData.absoConcentration}}</p>

                    </Col>
                    <Col span="4" class="table-td table-td-4">
                        <p>通风示意图</p>
                    </Col>
                    <Col span="8" class="table-td table-td-4">
                        <p >{{tableData.airflowDiagram}}</p>

                    </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td table-td-3"> <span> 伤亡损失 </span> </Col>
                    <Col span="4" class="table-td table-td-3">
                    <p class="table-td-inner">死亡人数</p>
                    <p class="table-td-inner">重伤人数</p>
                    <p class=" table-td-borderNone">轻伤人数</p>
                    </Col>
                    <Col span="4" class="table-td table-td-3">
                    <p class="table-td-inner">{{tableData.dead}}</p>
                    <p class="table-td-inner">{{tableData.seriousInjured}}</p>
                    <p class=" table-td-borderNone">{{tableData.slightWound}}</p>
                    </Col>
                    <Col span="4" class="table-td table-td-3">
                    <p class="table-td-inner">直接经济损失</p>
                    <p class="table-td-inner">波及范围</p>
                    <p class=" table-td-borderNone">停产时间（天）</p>
                    </Col>
                    <Col span="8" class="table-td table-td-3">
                    <p class="table-td-inner">{{tableData.moneyLost}}</p>
                    <p class="table-td-inner">{{tableData.affectArea}}</p>
                    <p class=" table-td-borderNone">{{tableData.stopDays}}</p>
                    </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td"> <span> 事故预兆 </span> </Col>
                    <Col span="20" class="table-td"> <span> {{tableData.indication}} </span> </Col>
                </Row>
                <Row class="for-border-left" v-if="showRow=='gasExplosion'">
                    <Col span="4" class="table-td table-td-char">
                        <p> 事故特征 </p>
                        <p> 瓦斯爆炸 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char-1R">
                        <p class="table-td-name"> 瓦斯积聚因：</p>
                        <p class="table-td-val"> {{tableData.gasAccReason}} </p>
                        <p class="table-td-name"> 点火源： </p>
                        <p class="table-td-val"> {{tableData.fireSource}} </p>
                        <p class="table-td-name" > 特征描述： </p>
                        <p class="table-td-val"> {{tableData.exDiscrib}} </p>

                    </Col>
                </Row>
                <Row class="for-border-left" v-if="showRow=='gasPoisioning'">
                    <Col span="4" class="table-td table-td-char">
                        <p> 事故特征 </p>
                        <p> 瓦斯中毒 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char-1R">
                        <p class="table-td-name"> 瓦斯浓度超限地点及浓度：</p>
                        <p class="table-td-val"> {{tableData.maxGasPosition}} </p>
                        <p class="table-td-name"> 特征描述： </p>
                        <p class="table-td-val"> {{tableData.poisionDescrib}} </p>
                    </Col>
                </Row>
                <Row class="for-border-left" v-if="showRow=='coalAndGasOutburst'">
                    <Col span="4" class="table-td table-td-char">
                        <p> 事故特征 </p>
                        <p> 瓦斯突出 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char">
                        <p class="table-td-name">突出类型：</p>
                        <p class="table-td-val"> {{tableData.maxGasPosition}} </p>
                        <p class="table-td-name"> 喷出煤岩量（吨）：  </p>
                        <p class="table-td-val"> {{tableData.poisionDescrib}} </p>
                        <p class="table-td-name"> 喷出距离（m）： </p>
                        <p class="table-td-val"> {{tableData.poisionDescrib}} </p>
                        <br>
                        <p class="table-td-name">    堆积坡度（°）：  </p>
                        <p class="table-td-val"> {{tableData.poisionDescrib}} </p>
                        <p class="table-td-name"> 喷出煤的粒度和分选情况：  </p>
                        <p class="table-td-val"> {{tableData.poisionDescrib}} </p>
                        <p class="table-td-name"> 特征描述： </p>
                        <p class="table-td-val"> {{tableData.poisionDescrib}} </p>
                    </Col>
                </Row>
                <Row class="for-border-left" v-if="showRow=='water'">
                    <Col span="4" class="table-td table-td-char">
                        <p> 事故特征 </p>
                        <p> 水害 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char">
                        <p class="table-td-name">突水水源： </p>
                        <p class="table-td-val"> {{tableData.waterSource}} </p>
                        <p class="table-td-name"> 突水通道：  </p>
                        <p class="table-td-val"> {{tableData.waterTunnel}} </p>
                        <p class="table-td-name">   水害发生部位：  </p>
                        <p class="table-td-val"> {{tableData.waterPosition}} </p>
                        <br>
                        <p class="table-td-name"> 突水量（m3/h）： </p>
                        <p class="table-td-val"> {{tableData.waterVolume}} </p>
                        <p class="table-td-name"> 特征描述： </p>
                        <p class="table-td-val"> {{tableData.waterDescrib}} </p>
                    </Col>
                </Row>
                <Row class="for-border-left" v-if="showRow=='fire'">
                    <Col span="4" class="table-td table-td-char">
                    <p> 事故特征 </p>
                    <p> 火灾 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char-1R">
                    <p class="table-td-name"> 火灾分类： </p>
                    <p class="table-td-val"> {{tableData.fireClassify}} </p>
                    <p class="table-td-name"> 风流紊乱现象： </p>
                    <p class="table-td-val"> {{tableData.airTube}} </p>
                    <p class="table-td-name" > 特征描述： </p>
                    <p class="table-td-val"> {{tableData.fireDescrib}} </p>

                    </Col>
                </Row>
                <Row class="for-border-left" v-if="showRow=='roofCollapse'">
                    <Col span="4" class="table-td table-td-char">
                    <p> 事故特征 </p>
                    <p> 顶板垮塌 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char-1R">
                    <p class="table-td-name">垮塌煤量（吨）：  </p>
                    <p class="table-td-val"> {{tableData.collapsedVolume}} </p>
                    <p class="table-td-name"> 垮塌面积（m2）：    </p>
                    <p class="table-td-val"> {{tableData.collapsedArea}} </p>
                    <p class="table-td-name" > 特征描述： </p>
                    <p class="table-td-val"> {{tableData.collapsedDescrib}} </p>

                    </Col>
                </Row>
                <Row class="for-border-left" v-if="showRow=='hitPress'">
                    <Col span="4" class="table-td table-td-char">
                    <p> 事故特征 </p>
                    <p> 冲击地压 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char-1R">
                    <p class="table-td-name">冲击次数：    </p>
                    <p class="table-td-val"> {{tableData.hitTimes}} </p>
                    <p class="table-td-name"> 最大震级：    </p>
                    <p class="table-td-val"> {{tableData.maxShockLevel}} </p>
                    <p class="table-td-name" > 特征描述： </p>
                    <p class="table-td-val"> {{tableData.hitDescrib}} </p>

                    </Col>
                </Row>
                <Row class="for-border-left" v-if="showRow=='coalPowerEx'">
                    <Col span="4" class="table-td table-td-char">
                    <p> 事故特征 </p>
                    <p> 煤尘爆炸 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char-1R">
                    <p class="table-td-name">CO体积浓度（%）：     </p>
                    <p class="table-td-val"> {{tableData.coAccumu}} </p>
                    <p class="table-td-name" > 特征描述： </p>
                    <p class="table-td-val"> {{tableData.coalPowderDescrib}} </p>

                    </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td table-td-char">
                    <p> 事故特征 </p>
                    <p> 其他事故 </p>
                    </Col>
                    <Col span="20" class="table-td table-td-char-1R">
                    <p >{{tableData.otherIncidents}}  </p>

                    </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td"> <span> 过程描述 </span> </Col>
                    <Col span="20" class="table-td"> <span> {{tableData.progressDescrib}} </span> </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td"> <span> 事故原因 </span> </Col>
                    <Col span="20" class="table-td"> <span> {{tableData.incidentReason}} </span> </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td"> <span> 事故处理 </span> </Col>
                    <Col span="20" class="table-td"> <span> {{tableData.incidentProcess}} </span> </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td"> <span> 救援措施 </span> </Col>
                    <Col span="20" class="table-td"> <span> {{tableData.rescueProcess}} </span> </Col>
                </Row>
                <Row class="for-border-left">
                    <Col span="4" class="table-td table-td-pic"> <span> 事故图片 </span> </Col>
                    <Col span="20" class="table-td table-td-pic"> <span> {{tableData.incidentsPic}} </span> </Col>
                </Row>

            </div>
            <div class="backtoDatalist">
                <Button type="primary" @click="switchPageD()">返回数据列表</Button>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .accidentsDetails{
        width:100%;
        border:1px solid #F0F0F0;
        background: #EEEEEE;
    }
    .accidentsDetails-table{
        /*height:500px;*/
        width:1166px;
        margin:30px auto;
        border:1px solid #BFBCBC;
        border-radius: 5px;
        background: #ffffff;
        padding:10px;
    }
    .accidentsDetails-table .table-td{
        border:1px solid #BFBCBC;
        height:40px;
        line-height:40px;
        text-align: center;
        border-left:none;
        font-size: 14px;
        margin-top: -1px;
    }
    .accidentsDetails-table .table-td:hover{
        cursor: pointer;
        background: #E5E5E5;
    }
    .accidentsDetails-table .table-td-3{
        height:120px;
        line-height:120px;
    }

    .accidentsDetails-table .table-td-4{
        height:160px;
        line-height:160px;
    }
    .accidentsDetails-table .table-td-inner{
        border-bottom:1px solid #BFBCBC;
        height:40px;
        line-height:40px;
        text-align: center;
    }
    .table-td-borderNone{
        border-bottom:none;
        height:40px;
        line-height:40px;
        text-align: center;
    }
    .accidentsDetails-table .table-td-char{
        height:60px;
        line-height:28px;
        padding:0 15px;
    }
    .accidentsDetails-table .table-td-char-1R{
        height:60px;
        line-height:60px;
        padding:0 15px;
    }
    .accidentsDetails-table .table-td-val{
        min-width:160px;
        float: left;
        text-align: left;
    }
    .accidentsDetails-table .table-td-name{
        float: left;
    }
    .accidentsDetails-table .table-td-pic{
        height:300px;
        line-height:300px;
    }
    .backtoDatalist{
        width:1166px;
        height:30px;
        line-height:30px;
        text-align: right;
        margin:20px auto
    }
    .for-border-left{
        border-left:1px solid #BFBCBC;
    }
    .accidentsDetails-title{
        font-size: 18px;
        height:30px;
        line-height:30px;
        width:1160px;
        /*border:1px solid blue;*/
        margin:0 auto;
        font-weight:bold;
        margin-top: 30px;
    }

</style>

<script>
    import * as MUTATIONS from '../../../../store/mutations'

    export default{
        name: 'accidDetaiTable',
        data()  {
            return{
                tableData: {
                    claVal:'001',
                    levelVal:'002',
                    dateVal:'003',
                    addressVal:'004',
                    tunnelVal:'005',
                    supportVal:'006',
                    standHVal:'007',
                    buriDepVal:'008',
                    operationVal:'009',
                    coalFname:'010',
                    coalAngle:'011',
                    coalthickness:'012',
                    hardness:'013',
                    upperFormation:'014',
                    lowerForation:'015',
                    geoStructure:'016',
                    gasConcentration:'017',
                    maxConcentration:'018',
                    airVolume:'019',
                    absoConcentration:'020',
                    airflowDiagram:'021',
                    dead:'022',
                    seriousInjured:'023',
                    slightWound:'024',
                    moneyLost:'025',
                    affectArea:'026',
                    stopDays:'027',
                    indication:'028',
                    gasAccReason:'029',
                    fireSource:'030',
                    exDiscrib:'031',
                    maxGasPosition:'032',
                    poisionDescrib:'033',
                    waterSource:'034',
                    waterTunnel:'035',
                    waterPosition:'036',
                    waterVolume:'037',
                    waterDescrib:'038',
                    fireClassify:'039',
                    airTube:'040',
                    fireDescrib:'041',
                    collapsedVolume:'042',
                    collapsedArea:'043',
                    collapsedDescrib:'044',
                    hitTimes:'045',
                    maxShockLevel:'046',
                    hitDescrib:'047',
                    coAccumu:'048',
                    coalPowderDescrib:'049',
                    otherIncidents:'050',
                    progressDescrib:'051',
                    incidentReason:'052',
                    incidentProcess:'053',
                    rescueProcess:'054',
                    incidentsPic:'055'

                },
                showRow:''

            }
        },
        mounted:function(){
            let pageName=document.getElementsByClassName('commonLinks')[0].dataset.link;
            console.log(pageName);
            this.$set(this.$data,'showRow',pageName)
        },
        methods: {
            switchPageD: function(){
                this.$store.commit(MUTATIONS.detailsPageSwitch);  //切换事故详情页面
            }

        }

    }

</script>