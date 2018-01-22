<template>
    <div class="wrapper" @click="update" style="justify-content:center">
        <image :src="logoUrl" class="logo"></image>
        <text class="title">Hello {{target}}</text>
        <text class="desc">Now, let's use vue to build your weex app.</text>
        <text class="label">Vue.js Star Count</text>
        <text class="count">{{count}}</text>
    </div>
</template>

<style>
    .wrapper {
        align-items: center;
        margin-top: 120px;
    }

    .title {
        padding-top: 40px;
        padding-bottom: 40px;
        font-size: 48px;
    }

    .logo {
        width: 360px;
        height: 156px;
    }

    .desc {
        padding-top: 20px;
        color: #888;
        font-size: 24px;
    }

    .label {
        color: #666;
        text-align: center;
        font-size: 60px;
    }

    .count {
        color: #41B883;
        text-align: center;
        font-size: 100px;
        margin-top: 80px;
        margin-bottom: 100px;
    }
</style>

<script>
    const stream = weex.requireModule('stream');
    export default {
        data() {
            return {
                logoUrl: 'http://img1.vued.vanthink.cn/vued08aa73a9ab65dcbd360ec54659ada97c.png',
                target: 'World',
                count: 'fetching...'
            }
        },
        created() {
            stream.fetch({
                method: 'GET',
                type: 'json',
                url: 'https://api.github.com/repos/vuejs/vue'
            }, res => {
                if (res.ok) {
                    this.count = res.data.stargazers_count
                } else {
                    this.count = '- unknown -'
                }
            })
        },
        methods: {
            update: function (e) {
                this.target = 'Weex';
                console.log('target:', this.target)
            }
        }
    }
</script>