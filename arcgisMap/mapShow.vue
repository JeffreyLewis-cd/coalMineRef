<template>
    <section class="container">
        <div>
            <Button type="info" @click="clickSwitchBtn" data-basemap="image">影像底图</Button>
            <Button type="info" @click="clickSwitchBtn" data-basemap="streets">街道底图</Button>
        </div>
        <div id="viewDiv">


        </div>
    </section>
</template>
<script>
    import * as esriLoader from 'esri-loader'
    import Vue from 'vue'
    import {mapGetters} from 'vuex'
    import * as MUTATIONS from '../../../store/mutations'

    export default{
        data(){
            return{

            }
        },
        mounted() {
            if (!esriLoader.isLoaded()) {
                esriLoader.bootstrap((err) => {
                    if (err) {
                        console.error(err)
                    }
                    this.createMap()
                }, {
                    url: 'https://js.arcgis.com/4.5/'
                })
            } else {
                this.createMap()
            }
        },
        methods: {
            createMap: function () {
                esriLoader.dojoRequire([
                    'esri/WebMap',
                    "esri/Map",
                    "esri/Basemap",
                    'esri/views/MapView',
                    "esri/Graphic",
                    "esri/geometry/Point",
                    "esri/geometry/Polyline",
                    "esri/geometry/Polygon",
                    "esri/symbols/SimpleMarkerSymbol",
                    "esri/symbols/SimpleLineSymbol",
                    "esri/symbols/SimpleFillSymbol",
                    "esri/layers/TileLayer",
                    "esri/layers/GraphicsLayer",
                    "esri/layers/FeatureLayer",
                    "dojo/domReady!"
                ],(WebMap,Map,Basemap, MapView,
                   Graphic, Point, Polyline, Polygon,
                   SimpleMarkerSymbol, SimpleLineSymbol, SimpleFillSymbol,TileLayer,GraphicsLayer,FeatureLayer) => {

                    //底图
                   let oCommunityLayer = new TileLayer({
                       url: "http://www.arcgisonline.cn/ArcGIS/rest/services/ChinaOnlineCommunity/MapServer"
                   });
                   let oImageLayer = new TileLayer({
                       url: "http://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer"
                   });

                   let activeBaselayer;

                    //切换底图
                    (this.activeBaselayer)?activeBaselayer=oImageLayer: activeBaselayer=oCommunityLayer;

                    let oImageBasemap = new Basemap({
                        baseLayers: [activeBaselayer]
                    });
                    let vueMap = new Map({
                        basemap: oImageBasemap,
                        logo: false
                    });
                    let view = new MapView({
                        container: 'viewDiv',
                        center: [104.06, 30.65],
                        zoom: 6,
                        locale: 'zh-cn',
                        map:vueMap
                    }) ;

                    //image底图才执行这个函数
                    if(this.activeBaselayer){
                        this.imageBaseMapAddlayers(vueMap,TileLayer)
                    }

                    this.addGraphics(view,Graphic, Point, Polyline, Polygon,SimpleMarkerSymbol, SimpleLineSymbol, SimpleFillSymbol)

                })
            },

            imageBaseMapAddlayers:function (vueMap,TileLayer) {
                //叠加图层-
                let oCityNameLayer = new TileLayer({
                    url: "http://services.arcgisonline.com/ArcGIS/rest/services/Reference/World_Boundaries_and_Places/MapServer"
                });

                vueMap.layers.addMany([oCityNameLayer]);
            },

            addGraphics:function (view,Graphic, Point, Polyline, Polygon,SimpleMarkerSymbol, SimpleLineSymbol, SimpleFillSymbol) {
                //添加 点， 线， 面 graphic
                let point = new Point({
                    longitude: 104.06,
                    latitude:  30.65
                });

                // Create a symbol for drawing the point
                let markerSymbol = new SimpleMarkerSymbol({
                    color: [226, 119, 40],
                    outline: { // autocasts as new SimpleLineSymbol()
                        color: [255, 255, 255],
                        width: 2
                    }
                });

                // Create a graphic and add the geometry and symbol to it
                let pointGraphic = new Graphic({
                    geometry: point,
                    symbol: markerSymbol
                });

                let polyline = new Polyline({
                    paths: [
                        [103.86, 30.02],
                        [105.60, 30.49],
                        [106.56, 29.51]
                    ]
                });

                // Create a symbol for drawing the line
                let lineSymbol = new SimpleLineSymbol({
                    color: [226, 119, 40],
                    width: 4
                });

                // Create an object for storing attributes related to the line
                let lineAtt = {
                    Name: "Keystone Pipeline",
                    Owner: "TransCanada",
                    Length: "3,456 km"
                };

                let polylineGraphic = new Graphic({
                    geometry: polyline,
                    symbol: lineSymbol,
                    attributes: lineAtt,
                    popupTemplate: { // autocasts as new PopupTemplate()
                        title: "{Name}",
                        content: [{
                            type: "fields",
                            fieldInfos: [{
                                fieldName: "Name"
                            }, {
                                fieldName: "Owner"
                            }, {
                                fieldName: "Length"
                            }]
                        }]
                    }
                });


                let polygon = new Polygon({
                    rings: [
                        [106.10, 30.78],
                        [107.51, 31.19],
                        [106.67, 30.42],
                        [106.10, 30.78]
                    ]
                });

                // Create a symbol for rendering the graphic
                let fillSymbol = new SimpleFillSymbol({
                    color: [227, 139, 79, 0.8],
                    outline: { // autocasts as new SimpleLineSymbol()
                        color: [255, 255, 255],
                        width: 1
                    }
                });

                // Add the geometry and symbol to a new graphic
                let polygonGraphic = new Graphic({
                    geometry: polygon,
                    symbol: fillSymbol
                });

                view.graphics.addMany([pointGraphic, polylineGraphic, polygonGraphic]);
            },

            //点击底图按钮，切换底图
            clickSwitchBtn: function(e) {
                let mapType1=e.target.dataset.basemap;
                let mapType2=e.target.parentNode.dataset.basemap;
                let mapType;
                (mapType1!=undefined)?mapType=String(mapType1):mapType=String(mapType2);

                if(mapType=='image'){
                    console.log('001');
                   this.$store.commit(MUTATIONS.imageBasemap);
                   this.createMap();

                }else {
                    console.log('002');
                    this.$store.commit(MUTATIONS.streetsBasemap);
                    this.createMap()
                }
            }

        },
        computed:{
            ...mapGetters({
                activeBaselayer:"activeBaselayer"
            })
        }
    }
</script>
<style scoped>
    @import url('https://js.arcgis.com/4.4/esri/css/main.css');

    #viewDiv {
        height:  600px;
        width:  100%;
        border:1px solid blue;
        background: #ffffff;
        margin-top: 10px;
    }
    .container{

    }
</style>