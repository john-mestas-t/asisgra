<script setup>
import { ref, onMounted } from 'vue';

const canvas = ref(null);
const videos = ref(null);
const ctx = ref(null);

const constraints = ref({
    audio: false,
    video: true
});

onMounted( async () => {
    if(video.value && canvas.value){
        ctx.value = canvas.getContext("2d");

        await navigator.mediaDevices
            .getUserMedia(constraints.value)
            .then(SetStream)
            .catch( e => {
                console.log(e);
            })
    }
})

function SetStream (stream){
    video.value.srcObject = stream;
    video.value.play();

    requestAnimationFrame(Draw);
}

function Draw(){
    ctx.value.drawImage(video.value, 0, 0, canvas.value.width, canvas.value.height);

    requestAnimationFrame(Draw);
}

</script>

<template>
    <div>
        <video ref="video" autoplay playsinline webkit-playsinline muted hidden></video>

        <canvas ref="canvas" width="1100" height="720" class="bg-black rounded-3x1"></canvas>

        <div class="items-center justify-center py-4">
            <button class="
                px-6 bg-green-500 rounded
                text-white text-2x1 uppercase font-bold
                hover:bg-green-600
            ">
                Take Picture
            </button>
        </div>
    </div>
</template>