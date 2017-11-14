
<template>
    <div class="enterpriseInfor-index commonLinks" data-pageindex="1" :data-link="linkCodeBox.coalSample">
        <!--2.2中间正文-->
        <div class="coalMineInformation">
            <div class="inforSearch-form">
                <div class="inforSearch-form-stable">
                    <div class="inforSearch-form-row">
                        <Row>
                            <Col span="24" class="inforSearch-form-title">煤样信息查询</Col>
                        </Row>
                        <Breadcrumb class="inforSearch-form-breadcrumb">
                            <span>当前位置：</span>
                            <Breadcrumb-item class="inforSearch-form-breadcrumb-item" href="/coalFormation">煤矿信息</Breadcrumb-item>
                            <Breadcrumb-item class="inforSearch-form-breadcrumb-item" href="/coalFormation">煤层地质信息</Breadcrumb-item>
                            <Breadcrumb-item class="inforSearch-form-breadcrumb-item">煤样信息</Breadcrumb-item>
                        </Breadcrumb>
                    </div>
                    <div class="inforSearch-form-row coalMineInfor-public">
                        <Row>
                            <Col span="24">
                            <Button class="about-area public-select-btn">选择地区</Button>
                            <VDistpicker class=" about-area vue-distpicker"></VDistpicker>
                            </Col>

                        </Row>
                    </div>
                </div>
                <!--更多条件公共组件-->
                <getMoreConditions></getMoreConditions>
                <staticAnalysis></staticAnalysis>

            </div>

        </div>
        <div class="coalMineInformation-body">
            <showDataList ></showDataList>
        </div>

    </div>

</template>

<script>
    import Vue from 'vue'
    import getMoreConditions from '../../../publicInforSearch/getMoreConditions.vue'
    import VDistpicker from 'v-distpicker'
    import showDataList from '../../../publicInforSearch/showDataList.vue'
    import {mapGetters} from 'vuex'
    import staticAnalysis from '../../../publicInforSearch/staticAnalysis.vue'


    export default{
        name: 'coalSample',
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
            staticAnalysis
        },
        computed: {
                ...mapGetters({
                    listShow: 'listShow',
                    linkCodeBox:'linkCodeBox'

                })
    }
    }



</script>

<style scoped>

    @import "../../../../../assets/css/init-css.css";




</style>