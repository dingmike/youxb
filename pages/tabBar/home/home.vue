<template>
    <view class="uni-common-pb">

        <view class="page-section swiper">
            <view class="page-section-spacing">
                <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
                        :duration="duration">
                    <swiper-item>
                        <view class="swiper-item">
                            <a href="http://mp.weixin.qq.com/s/-n9bWkyE_oSEpdZELnUFog">
                                <img style="width: 100%" src="../../../static/banner/banner.png?v=1" alt="">
                            </a>
                        </view>
                    </swiper-item>
                    <swiper-item>
                        <view class="swiper-item">
                            <a href="http://mp.weixin.qq.com/s/-n9bWkyE_oSEpdZELnUFog">
                                <img style="width: 100%" src="../../../static/banner/banner3.png" alt="">
                            </a>
                        </view>
                    </swiper-item>
                    <swiper-item>
                        <view class="swiper-item">
                            <a href="http://mp.weixin.qq.com/s/-n9bWkyE_oSEpdZELnUFog">
                                <img style="width: 100%" src="../../../static/banner/banner2.png" alt="">
                            </a>
                        </view>
                    </swiper-item>
                </swiper>
            </view>
        </view>

        <view class="own-card">
            <view class="uni-flex uni-row">
                <view class="flex-item own-item">
                    <view class="own-num">0</view>
                    <view>油币</view>
                </view>
                <view class="flex-item own-item">
                    <view class="own-num">0.00</view>
                    <view>信用额度</view>
                </view>
            </view>
        </view>

        <view class="uni-card">
            <view class="uni-grid-9 uni-common-mt own-bg-white">
                <view class="uni-grid-9-item" hover-class="uni-grid-9-item-hover" v-for="(item,index) in grids" :key="index" :class="index % 3 === 2 ? 'no-border-right' : ''">
                    <image class="uni-grid-9-image" :src="item.pic"></image>
                    <text class="uni-grid-9-text own-grid-9-text">{{item.text}}</text>
                </view>
            </view>
        </view>

        <view class="uni-flex uni-row own-bg-white own-card-padding">
            <view class="uni-flex uni-column">
                <image src="../../../static/banner/content_banner_shouchong.png" style="width: 324upx;height: 316upx;"></image>
            </view>
            <view class="uni-flex uni-column">
                <view class="uni-flex uni-row">
                    <image src="../../../static/banner/content_banner_shuaka.png" style="height: 150upx;width:320upx;padding: 0 32upx 20upx 32upx;"></image>
                </view>
                <view class="uni-flex uni-row">
                    <view class="text">
                        <image src="../../../static/banner/content_banner_butie.png" style="height: 150upx; width: 320upx;padding: 0 32upx 0upx 32upx;"></image>
                    </view>
                </view>
            </view>
        </view>




       <!-- <view class="uni-card" v-for="(list,index) in lists" :key="index">
            <view class="uni-list">
                <view class="uni-list-cell uni-collapse">
                    <view class="uni-list-cell-navigate uni-navigate-bottom" hover-class="uni-list-cell-hover"
                          :class="list.open ? 'uni-active' : ''"
                          @click="triggerCollapse(index)">
                        {{list.name}}
                    </view>
                    <view class="uni-list uni-collapse" :class="list.open ? 'uni-active' : ''">
                        <view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,key) in list.pages"
                              :key="key" :url="item.url"
                              @click="goDetailPage(item.url)">
                            <view class="uni-list-cell-navigate uni-navigate-right"> {{item.name}}</view>
                        </view>
                    </view>
                </view>
            </view>
        </view>-->



    </view>
</template>
<script>
    export default {
        data() {
            // 暂时这么写，后面看怎么优化。
            let mediaPages = [{
                name: '图片',
                url: 'image'
            },
                // #ifdef APP-PLUS || MP-WEIXIN || MP-BAIDU
                {
                    name: '录音',
                    url: 'voice'
                }, {
                    name: '背景音频',
                    url: 'background-audio'
                },
                // #endif
                // #ifndef MP-ALIPAY
                {
                    name: '视频',
                    url: 'video'
                },
                // #endif
                // #ifndef H5
                {
                    name: '文件',
                    url: 'file'
                },
                // #endif
            ];

            const list = [{
                id: 'page',
                name: '界面',
                open: false,
                pages: [{
                    name: '设置界面标题',
                    url: 'set-navigation-bar-title'
                }, {
                    name: '页面跳转',
                    url: 'navigator'
                }, {
                    name: '下拉刷新',
                    url: 'pull-down-refresh'
                },
                    //#ifndef H5
                    {
                        name: '创建动画',
                        url: 'animation'
                    },
                    //#endif
                    {
                        name: '创建绘画',
                        url: 'canvas'
                    },
                    {
                        name: '显示操作菜单',
                        url: 'action-sheet'
                    }, {
                        name: '显示模态弹窗',
                        url: 'modal'
                    }, {
                        name: '显示加载提示框',
                        url: 'show-loading'
                    }, {
                        name: '显示消息提示框',
                        url: 'toast'
                    }
                ]
            }, {
                id: 'device',
                name: '设备',
                open: false,
                pages: [{
                    name: '获取手机网络状态',
                    url: 'get-network-type'
                }, {
                    name: '获取手机系统信息',
                    url: 'get-system-info'
                }, {
                    name: '打电话',
                    url: 'make-phone-call'
                },
                    //#ifndef H5
                    {
                        name: '扫码',
                        url: 'scan-code'
                    }, {
                        name: '剪贴板',
                        url: 'clipboard'
                    },
                    //#endif
                    {
                        name: '监听加速度传感器',
                        url: 'on-accelerometer-change'
                    }, {
                        name: '监听罗盘数据',
                        url: 'on-compass-change'
                    },
                    //#ifdef APP-PLUS
                    {
                        name: '监听距离传感器',
                        url: '/platforms/app-plus/proximity/proximity'
                    }, {
                        name: '监听方向传感器',
                        url: '/platforms/app-plus/orientation/orientation'
                    }
                    //#endif
                ]
            }, {
                id: 'network',
                name: '网络',
                open: false,
                pages: [{
                    name: '发起一个请求',
                    url: 'request'
                }, {
                    name: '上传文件',
                    url: 'upload-file'
                }, {
                    name: '下载文件',
                    url: 'download-file'
                }]
            }, {
                id: 'media',
                name: '媒体',
                open: false,
                pages: mediaPages
            }, {
                id: 'location',
                name: '位置',
                open: false,
                pages: [{
                    name: '获取当前位置',
                    url: 'get-location'
                }, {
                    name: '使用地图查看位置',
                    url: 'open-location'
                }, {
                    name: '使用地图选择位置',
                    url: 'choose-location'
                }]
            }, {
                id: 'storage',
                name: '数据',
                open: false,
                pages: [{
                    name: '数据存储',
                    url: 'storage'
                }]
            },
                // #ifndef H5
                {
                    id: 'login',
                    name: '登录',
                    open: false,
                    pages: [{
                        name: '登录',
                        url: 'login'
                    }, {
                        name: '获取用户信息',
                        url: 'get-user-info'
                    }]
                },
                {
                    id: 'share',
                    name: '分享',
                    open: false,
                    pages: [{
                        name: '分享',
                        url: 'share'
                    }]
                },
                // #endif
                // #ifdef APP-PLUS || MP-WEIXIN
                {
                    id: 'payment',
                    name: '支付',
                    open: false,
                    pages: [{
                        name: '发起支付',
                        url: 'request-payment'
                    }]
                },
                // #endif
                // #ifdef APP-PLUS
                {
                    id: 'speech',
                    name: '语音',
                    open: false,
                    pages: [{
                        name: '语音识别',
                        url: '/platforms/app-plus/speech/speech'
                    }]
                }, {
                    id: 'push',
                    name: '推送',
                    open: false,
                    pages: [{
                        name: '推送',
                        url: '/platforms/app-plus/push/push'
                    }]
                },
                //#endif
            ];
            return {
                lists: list,
                title: 'swiper',
                background: ['color1', 'color2', 'color3'],
                indicatorDots: true,
                autoplay: true,
                interval: 2000,
                duration: 500,
                grids:[
                    {pic: '../../../static/banner/icon_youkachongzhi.png',text: '油卡充值'},
                    {pic: '../../../static/banner/icon_youhuiquan.png',text: '优惠券'},
                    {pic: '../../../static/banner/icon_xinyongjiayou.png',text: '信用加油'},
                    {pic: '../../../static/banner/icon_liantongzhuanxiang.png',text: '联通专享'},
                    {pic: '../../../static/banner/icon_zaixianshangcheng.png',text: '在线商城'},
                    {pic: '../../../static/banner/icon_goumaiyouquan.png',text: '无卡加油'}
                ]
            }
        },
        onShareAppMessage() {
            return {
                title: '欢迎体验uni-app',
                path: '/pages/tabBar/API/API'
            }
        },
        onNavigationBarButtonTap(e) {
            uni.navigateTo({
                url: '/pages/about/about'
            });
        },
        methods: {
            triggerCollapse(e) {
                if (!this.lists[e].pages) {
                    this.goDetailPage(this.lists[e].url);
                    return;
                }
                for (var i = 0; i < this.lists.length; ++i) {
                    if (e === i) {
                        this.lists[i].open = !this.lists[e].open;
                    } else {
                        this.lists[i].open = false;
                    }
                }
            },
            goDetailPage(e) {
                let url = ~e.indexOf('platform') ? e : '/pages/API/' + e + '/' + e;
                uni.navigateTo({
                    url: url
                })
            }

        }
    }
</script>

<style>
    page {
        height: auto;
        min-height: 100%;
    }

    .uni-card {
        box-shadow: none;
    }

    .uni-list:after {
        height: 0;
    }

    .uni-list:before {
        height: 0;
    }
    .own-card{
        height: 108upx;
        padding-top: 8upx;
        /* left: 54px; */
        background: #fff;
    }
    .own-item{
        width: 50%;
        text-align: center;
    }
    .own-num{
        font-size: 32upx ;
        font-weight: 800;
    }
    .own-grid-9-text{
        line-height: 48upx;
        font-size: 28upx;
    }
    .own-bg-white{
        background: #fff;
    }
    .own-card-padding{
        padding: 16upx 20px;
    }
</style>
