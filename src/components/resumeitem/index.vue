<!--
 * @Author: luohong
 * @Date: 2019-09-02 11:03:15
 * @LastEditors: luohong
 * @LastEditTime: 2019-09-05 17:21:13
 * @Description: 
 * @email: 3300536651@qq.com
 -->
<template>
    <div>
        <a-card :bordered=false :hoverable=false class="template-preview">
            <div>
                <img :src="imgUrl" width="100%" height="200" alt="templatePreview" />
    
            </div>
            <a-card-meta :title="title" :description="description">
            </a-card-meta>
            <div class="mask">
                <a-button type="default" class="btn" size="small" @click="preview(id)">预览</a-button>
            </div>
        </a-card>
        <a-modal v-model="visible" title="预览" onOk="handleOk" width="95%" :bodyStyle="{position:'relative'}">
            <template slot="footer">
                                                                <a-button key="submit" type="primary" :loading="loading" @click="handleOk">
                                                                使用模版
                                                                </a-button>
</template>
        <div class="resume-mask">
        </div>    
            <component v-bind:is="currentTabComponent"></component>
        </a-modal>
    </div>
</template>

<script>
    import Template1 from '@components/template/template1';
    import Template2 from '@components/template/template2';
    export default {
        name: 'resumeitem',
        props: {
            title: {
                type: String,
                default: '前端模版'
            },
            imgUrl: String,
            id: {
                stype: String,
                default: 1
            },
            description: String
        },
        data() {
            return {
                loading: false,
                visible: false,
            }
        },
        methods: {
            preview(id) {
                this.visible = true;
            },
            handleOk(e) {
                // 使用模版
                this.loading = true;
                setTimeout(() => {
                    this.visible = false;
                    this.loading = true;
                    this.$router.push(`/resumeEdit/${this.id}`);
                }, 0);
            }
        },
        computed: {
            currentTabComponent: function() {
                return 'resumeTemplate' + this.id
            }
        },
        components: {
            'resumeTemplate1': Template1
        }
    }
</script>

<style>
    .template-preview {
        position: relative;
    }
    
    .template-preview .mask {
        width: 100%;
        height: 100%;
        background: rgba(24, 144, 255, .7);
        box-sizing: border-box;
        transition: all .2s ease-in-out;
        position: absolute;
        left: 0;
        top: 0;
        visibility: hidden;
        transform: scale(0);
    }
    
    .template-preview .btn {
        visibility: visible;
        position: absolute;
        bottom: 10px;
        right: 10px;
        cursor: pointer;
        left: 50%;
        top: 50%;
        margin-left: -25px;
        margin-top: -12px;
    }
    
    .template-preview:hover .mask {
        transform: scale(1);
        visibility: visible;
    }
    
    .template-preview:hover .btn {
        visibility: visible;
    }
    
    .resume-mask {
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 9999;
    }
</style>