
<template>
    <div class="coalMineInfor-index commonLinks" data-pageindex="1"  :data-link="linkCodeBox.coalPowder">

        <!--2.2中间正文-->
        <div class="inforSearch-common">
            <div class="inforSearch-form">
                <div class="inforSearch-form-stable">
                    <div class="inforSearch-form-row">
                        <Row>
                            <Col span="24" class="inforSearch-form-title">煤尘查询</Col>
                        </Row>
                        <Breadcrumb class="inforSearch-form-breadcrumb">
                            <span>当前位置：</span>
                            <Breadcrumb-item class="inforSearch-form-breadcrumb-item" href="/fireInfor">灾害事故信息</Breadcrumb-item>
                            <Breadcrumb-item class="inforSearch-form-breadcrumb-item" href="/fireInfor">煤尘事故</Breadcrumb-item>
                            <Breadcrumb-item class="inforSearch-form-breadcrumb-item">煤尘</Breadcrumb-item>
                        </Breadcrumb>
                    </div>
                    <div class="inforSearch-form-row coalMineInfor-public">
                        <Row>

                            <Col span="12">
                            <Input class="accidentName pubConditionInput">
                            <span slot="prepend">事故名称</span>
                            </Input>
                            </Col>
                            <Col span="12">
                            <Input class="accidentPlace pubConditionInput">
                            <span slot="prepend">事故地点</span>
                            </Input>
                            </Col>
                            <Col span="12" class="accident-dateRange">
                            <Button class="public-select-btn">事故时间</Button>
                            <Date-picker type="daterange" :options="options2" placement="bottom-start" placeholder="选择日期"
                                         class="selectAreaStyle user-select-date"></Date-picker>
                            </Col>

                        </Row>
                    </div>
                </div>
                <!--更多条件公共组件-->
                <getMoreConditions></getMoreConditions>
                <staticAnalysis></staticAnalysis>
            </div>

        </div>
        <div class="inforSearch-common-body">
            <accidDetaiTable v-if="detailsPage"></accidDetaiTable>
            <showDataList v-if="dataListPage"></showDataList>
        </div>
    </div>

</template>

<script>
    import Vue from 'vue'
    import getMoreConditions from '../../publicInforSearch/getMoreConditions.vue'
    import VDistpicker from 'v-distpicker'
    import showDataList from '../../publicInforSearch/showDataList.vue'
    import {mapGetters} from 'vuex'
    import accidDetaiTable from '../publicAccidents/accidDetaiTable.vue'
    import staticAnalysis from '../../publicInforSearch/staticAnalysis.vue'


    export default{
        name: 'coalPowder',
        data () {
            return {
                options2: {
                    shortcuts: [
                        {
                            text: '最近一周',
                            value () {
                                const end = new Date();
                                const start = new Date();
                                start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
                                return [start, end];
                            }
                        },
                        {
                            text: '最近一个月',
                            value () {
                                const end = new Date();
                                const start = new Date();
                                start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
                                return [start, end];
                            }
                        },
                        {
                            text: '最近三个月',
                            value () {
                                const end = new Date();
                                const start = new Date();
                                start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
                                return [start, end];
                            }
                        }
                    ]
                }
            }
        },
        components: {
            getMoreConditions,
            VDistpicker,
            showDataList,
            accidDetaiTable,
            staticAnalysis
        },
        computed: {
                ...mapGetters({
                    listShow: 'listShow',
                    detailsPage:'detailsPage',
                    dataListPage:'dataListPage',
                    linkCodeBox:'linkCodeBox'

                })
    }
    }



</script>

<style scoped>

    @import "../../../../assets/css/init-css.css";




</style>
