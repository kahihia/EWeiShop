<template>
    <div class='renovation--show-swiper-box'>
        <div class='show-swiper'>
            <swiper :options="swiperOption" ref="mySwiper">
                <!-- slides -->
                <swiper-slide v-for='item in imgList' :key='item.img'><img :src='item.img' :alt="item.alt" :style='{marginBottom:item.title?"32px":"10px"}'><span :style='{transform:isIOS?"scale(0.7)":"scale(0.93)",bottom:isIOS?"-5px":"0"}'>{{item.title}}</span></swiper-slide>
            </swiper>
        </div>
        <div class="show-swiper__pagination">
            <span v-for='item in imgList.length' :key='item' class="show-swiper__pagination__item" :style='{backgroundColor:item==active+1?paginationColor:"#ddd"}' :class='{"show-swiper__pagination__item--active":item==active+1}'></span>
        </div>
    </div>
</template>

<script>
    import {
        Button,
        Cell
    } from 'vant';
    import {
        swiper,
        swiperSlide
    } from 'vue-awesome-swiper'
    export default {
        props: {
            imgList: {
                type: Array,
                default () {
                    return [{
                        img: '/static/image/renovation/template1.jpg',
                        alt: '门店装修模板',
                        title: ''
                    }, {
                        img: '/static/image/renovation/template2.jpg',
                        alt: '门店装修模板',
                        title: ''
                    }, {
                        img: '/static/image/renovation/template3.jpg',
                        alt: '门店装修模板',
                        title: ''
                    }, {
                        img: '/static/image/renovation/template4.jpg',
                        alt: '门店装修模板',
                        title: ''
                    }]
                }
            },
            paginationColor: {
                type: String,
                default: '#49daae'
            }
        },
        components: {
            Button,
            Cell,
            swiper,
            swiperSlide
        },
        beforeMount() {
            var u = navigator.userAgent,
                app = navigator.appVersion;
            var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1; //g
            this.isIOS = !isAndroid;
        },
        data() {
            let that = this;
            return {
                isIOS: false,
                active: 0,
                swiperOption: {
                    slidesPerView: 3,
                    notNextTick: true,
                    // swiper configs 所有的配置同swiper官方api配置
                    autoplay: false,
                    resistanceRatio: 0,
                    // slideToClickedSlide: true,
                    // direction : 'vertical',
                    // effect: "coverflow",
                    loop: true,
                    initialSlide: 1,
                    grabCursor: true,
                    setWrapperSize: true,
                    spaceBetween: 0,
                    centeredSlides: true,
                    // autoHeight: true,
                    // paginationType:"bullets",
                    paginationClickable: false,
                    mousewheelControl: true,
                    observeParents: true,
                    on: {
                        slideChangeTransitionStart: function() {
                            that.active = Math.abs(this.activeIndex - 1) % that.imgList.length;
                            that.$emit('activeIndex', this.activeIndex)
                        },
                    },
                    // some swiper options...
                }
            }
        },
        computed: {
            swiper() {
                return this.$refs.mySwiper.swiper
            }
        },
        mounted() {
            // current swiper instance
            // 然后你就可以使用当前上下文内的swiper对象去做你想做的事了
            // this.swiper.slideTo(3, 1000, false)
        }
    }
</script>

<style lang='scss'>
    .renovation--show-swiper-box {
        overflow: hidden;
        width: 100%;
        .show-swiper {
            width: 1612px;
            margin: 30px 0 46px;
            position: relative;
            top: 0;
            left: 50%;
            transform: translate(-50%, 0);
            .swiper-container {
                // height: 890px;
                overflow: visible;
                .swiper-slide {
                    img {
                        display: block;
                        width: 500px;
                        height: 890px;
                        margin: 0 auto;
                        transition: all .5s;
                        opacity: 0.6;
                        border-radius: 10px;
                        box-shadow: 0 4px 24px rgba(0, 0, 0, 0.1);
                    }
                    span {
                        position: absolute;
                        bottom: 0px;
                        transition: all .5s;
                        opacity: 0.5;
                        left: 0;
                        width: 100%;
                        font-size: 24px;
                        text-align: center;
                        line-height: 24px;
                        color: #5d6494; // transform: scale(.7);
                    }
                }
                .swiper-slide-active {
                    img {
                        opacity: 1;
                    }
                    span {
                        // bottom: 0;
                        opacity: 1;
                    }
                }
            }
        }
        >.show-swiper__pagination {
            height: 7px;
            bottom: 0;
            position: absolute;
            width: 100%;
            text-align: center;
            display: flex;
            justify-content: center;
            >.show-swiper__pagination__item {
                height: 100%;
                width: 48px;
                background: #ddd;
                margin: 0 12px;
                border-radius: 6px;
            }
            >.show-swiper__pagination__item--active {
                background: #49daae;
            }
        }
    }
</style>