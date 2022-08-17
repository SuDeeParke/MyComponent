<!--
 * @Author: sudongpeng sudongpeng@uino.com
 * @Date: 2022-08-12 14:30:18
 * @Description:组件 实时直播窗口
-->
<template>
    <section class="live-view">
        <video
            id="player"
            ref="vedioDom"
            :class="{ 'video-js': !isFlv }"
            controls
            muted
            autoplay
            v-if="!props.static"></video>
        <div v-else class="fake-vedio">
            <img :src="props.url">
        </div>
    </section>
</template>

<script setup lang="ts">
import flvjs from 'flv.js'
import  videojs from 'video.js';

const props = defineProps({
    url: {
        type: String,
        default: '',
    },
    static: {
        type: Boolean,
        default: false
    }
})

const vedioDom = ref()
const isFlv = computed(() => {
    return  /\.flv$/.test(props.url)
})
onMounted(() => {

    if (flvjs.isSupported() && !props.static && isFlv.value) {
        const flvPlayer = flvjs.createPlayer({
            type: 'flv',
            // isLive: true,
            url: props.url,
        })
        flvPlayer.attachMediaElement(vedioDom.value as HTMLMediaElement)
        flvPlayer.load()
        flvPlayer.play()
    }
    else {
        console.log('================m3u8================')
        const hlsPlayer = videojs(vedioDom.value, {
            width: `${418 - (21 + 22)}px`,
            height: `${718 - (26+25)}px`,
            sources: [
                {
                    src: props.url,
                    type: "application/x-mpegURL"
                },
            ],
        }, () => {
            hlsPlayer.play()
        })
    }
})

</script>

<style lang="scss" scoped>
.live-view {
    display: block;
    width: 418px;
    height: 718px;
    padding: 26px 21px 25px 22px;
    box-sizing: border-box;
    //   border: 1px solid rgb(123, 176, 212);
    border-radius: 10px;
    background: url('../assets/imgs/leftScreen/live_view_bg.png');
    background-size: 100% 100%;
    background-repeat: no-repeat;
    video, .fake-vedio {
        width: 100%;
        height: 100%;
        border-radius: 6px;
        background-color: #000000;
        object-fit: cover;
    }
    .fake-vedio{
        overflow: hidden;
        > img{
            width: 100%;
        }
    }
}
</style>
