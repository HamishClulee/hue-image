<template>
    <figure class="image-con">
        <img
            :src="placeholder"
            :id="`vue-image-${random}`"
            :data-src="imgsrc"
            :alt="alttag"
            width="100%"
        />
    </figure>
</template>

<script>
import { PLACEHOLDER } from './placeholder.js'
export default {
    name: 'hueimage',
    props: {
        imgsrc: {
            type: String,
            required: true,
        },
        placeholder: {
            type: String,
            required: false,
            default: PLACEHOLDER,
        },
        alttag: {
            type: String,
            required: true,
        },
        srcmap: Object,
    },
    data () {
        return {
            random: Math.floor((Math.random() * 99999999) + 1),
        }
    },
    mounted() {
        const imageObserver = new IntersectionObserver(entries => {
            if(entries[0].isIntersecting) {
                const lazyImage = entries[0].target
                if (this.srcmap) {
                    this.applysrcset(lazyImage)
                } else {
                    lazyImage.src = lazyImage.dataset.src
                }
            }
        });
        imageObserver.observe(document.getElementById(`vue-image-${this.random}`));
    },
    methods: {
        applysrcset(image) {
            image.setAttribute('srcset', `${this.srcmap['small']} 480w, ${this.srcmap['medium']} 1280w, ${this.srcmap['large']} 1980w`)
        }
    }
}
</script>
<style lang="sass" scoped>
img
    width: 100%
    object-fit: scale-down
figure
    margin: 0
    padding: 0
</style>
