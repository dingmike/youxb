<template>
    <view class="uni-common-pb">

        <view class="page-section">
            <view class="uni-center" style="background:#FFFFFF; font-size:0;">
                <image class="image" style="width: 100%;" mode="widthFix" src="../../../static/gasCard/banner_img.png"/>
            </view>
        </view>
        <view class="page-section">
            <view class="uni-cell-divider own-divider">
                领取油卡
            </view>
            <view class="uni-form-item uni-column">
                <view class="uni-center" style="background:#FFFFFF; font-size:0;">
                    <image class="image" style="width: 100%; height: 320upx;" mode="aspectFit" src="../../../static/gasCard/img_erweima.png"/>

                </view>
                <text style="font-size:24upx;text-align: center ;background:#ffffff; color: red;">您可以识别二维码或者扫描渠道二维码领取油卡</text>
            </view>
        </view>

        <view class="page-section">
            <view class="uni-cell-divider own-divider">
                绑定油卡
            </view>
            <view class="uni-form-item uni-column">
                <label class="uni-list-cell uni-list-cell-pd own-bg-white own-label-padding">
                    <view class="title">油卡卡号:</view>
                    <view>
                        <label class="label-2-text">
                            <input class="uni-input" type="number" placeholder="请输入卡号" />
                        </label>
                    </view>
                </label>
                <label class="uni-list-cell uni-list-cell-pd own-bg-white own-label-padding">
                    <view class="title">确认卡号:</view>
                    <view>
                        <label class="label-2-text">
                            <input class="uni-input" type="number" placeholder="请再次输入卡号" />
                        </label>
                    </view>
                </label>
            </view>
            <view class="uni-form-item uni-column own-divider">
                <span><uni-icon size="20" type="info" color="red"></uni-icon>
说明：每月10号为出账单日</span>
            </view>
            <view class="own-divider own-bg-white">
                <button style="background: orangered;color: #fff;">绑定油卡</button>
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
    import uniIcon from '../../../components/uni-icon.vue'
    export default {
        components: {
            uniIcon
        },
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
                info:"info",
                lists: list,
                title: 'swiper',
                background: ['color1', 'color2', 'color3'],
                indicatorDots: true,
                autoplay: true,
                interval: 2000,
                duration: 500,
                grids: [
                    {pic: '../../../static/banner/icon_youkachongzhi.png', text: '油卡充值'},
                    {pic: '../../../static/banner/icon_youhuiquan.png', text: '优惠券'},
                    {pic: '../../../static/banner/icon_xinyongjiayou.png', text: '信用加油'},
                    {pic: '../../../static/banner/icon_liantongzhuanxiang.png', text: '联通专享'},
                    {pic: '../../../static/banner/icon_zaixianshangcheng.png', text: '在线商城'},
                    {pic: '../../../static/banner/icon_goumaiyouquan.png', text: '无卡加油'}
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

    .own-card {
        height: 108 upx;
        padding-top: 8 upx;
        /* left: 54px; */
        background: #fff;
    }

    .own-item {
        width: 50%;
        text-align: center;
    }

    .own-num {
        font-size: 32 upx;
        font-weight: 800;
    }

    .own-grid-9-text {
        line-height: 48 upx;
        font-size: 28 upx;
    }

    .own-bg-white {
        background: #fff;
    }

    .own-card-padding {
        padding: 16 upx 20px;
    }
    .own-divider{
        padding: 12upx 16upx;
    }
    .own-label-padding{
        padding: 16upx 16upx;
    }
</style>
