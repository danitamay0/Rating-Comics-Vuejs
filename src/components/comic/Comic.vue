<template>
    <b-row class="text-center article">
        <b-col cols="12">
            <h2 class="font-weight-bolder">#{{comic.num}} {{comic.title}}</h2>
        </b-col>
        <b-col cols="12">
            <img :src="comic.img" :alt="comic.alt" />
        </b-col>
        <b-col cols="12">
            <RatingStars></RatingStars>
        </b-col>
    
    </b-row>
</template>

<script>
import RatingStars from './RatingStars'

export default {
    name: 'Comic',
    components: {
        RatingStars,
    },
    props: {
        comic: {}
    }

}
</script>

<style scoped>
.article {
    background-color: #111;
    padding: 10px 10px;
    border-radius: 10px;
    transition: all 1s ease;
}

.article:hover {
    box-shadow: 0px 0px 20px rgba(23, 162, 184, .4)
}

img {
    max-height: 340px;
}
</style>
