<template>
    <div class='vip-manage-easier'>
        <swipe :autoplay="3000" style='height:100%;' indicator-color="white" @change="onChange">
            <swipe-item class='vip-manage-easier__swipe-item'>
                <img class='vip-manage-easier__img' v-lazy="'/static/image/distribution_scheme/img1.jpg'" alt="分销激励机制">
            </swipe-item>
            <swipe-item class='vip-manage-easier__swipe-item'>
                 <img  class='vip-manage-easier__img' v-lazy="'/static/image/distribution_scheme/img2.jpg'" alt="分销激励机制">
            </swipe-item>
            <div class="custom-indicator" slot="indicator">
                <span class="point point1" :class='{"active-point":current==0}'></span>
                <span class="point point2" :class='{"active-point":current==1}'></span>
            </div>
        </swipe>
    </div>
</template>

<script>
    import {
        Swipe,
        SwipeItem
    } from 'vant';
    export default {
        data() {
            return {
                current: 0,
                detailLeftAlign: {
                    textAlign: 'left'
                }
            }
        },
        methods: {
            onChange(index) { 
                this.current = index;
            }
        },
        components: { 
            Swipe,
            SwipeItem
        }
    }
</script>

<style scoped lang='scss'>
    .vip-manage-easier {
        background: #fff;
        overflow: hidden; // position: absolute;
        float: left;
        border-top-right-radius: 10px;
        border-top-left-radius: 10px;
        width: 100%;
        position: relative;
        height: 687px;
        .vip-manage-easier__img {
            width: 567px;
            display: block;
            margin: 50px auto 0;
            overflow: hidden;
        }
        .custom-indicator {
            width: 120px;
            position: absolute;
            bottom: 72px;
            left: 0;
            right: 0;
            margin: auto;
            >.point {
                width: 48px;
                height: 6px;
                border-radius: 3px;
                background: #ddd;
                float: left;
            }
            >.point2 {
                float: right;
            }
            >.active-point{
                 background: #f15f51;
            }
        }
    }
</style>