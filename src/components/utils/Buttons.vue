<template>
    <div class="text-center mb-2">
        <b-button @click="$emit('click',comicId-1)" :disabled="comicId==comicMinId" variant="outline-info">
            <i class="fas fa-chevron-left"></i> Anterior
    
        </b-button>
        <b-button @click="$emit('click')" class="ml-2 mr-2 " variant="outline-info">Buscar Aleatorio</b-button>
        <b-button @click="$emit('click',comicId+1)" :disabled="comicId==comicMaxId" variant="outline-info">Siguiente
            <i class="fas fa-chevron-right"></i>
        </b-button>
    </div>
</template>

<script>
export default {
    name: 'PreLoader',
    props: {
        comicId: Number,
        comicMinId: Number,
        comicMaxId: Number,
    }
}
</script>

