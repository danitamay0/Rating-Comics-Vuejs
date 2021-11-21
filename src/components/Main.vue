<template>
    <section class="container mb-4">
        <b-container class="bv-example-row">
            <b-row>
                <b-col cols="12" class="mb-4">
                    <PreLoader v-if="fetching==='pending'" label="Buscando Comic..."  />
                    <Comic v-if="fetching=='succeded'" :comic="comic"></Comic>
                </b-col>
                <b-col cols="12" >
                    <Buttons @click="search" :comicId="comicId" :comicMaxId="comicMaxId" :comicMinId="comicMinId"></Buttons>
                </b-col>
            </b-row>
        </b-container>
    
    </section>
</template>

<script>

import axios from "axios";
import Swal from 'sweetalert2'
import { uriBase } from "../enviroments"

import PreLoader from "./utils/PreLoader";
import Buttons from "./utils/Buttons";
import Comic from "./comic/Comic";


export default {
    name: 'Main',
    components: {
        Comic,
        PreLoader,
        Buttons
    },
    data: () => {
        return {
            comic: {},
            fetching: 'iddle',
            comicMaxId: 55,
            comicMinId: 1,
            comicId: null
        }
    },
    methods: {
        search: async function(idSearch = null) {
            this.comicId = idSearch ? idSearch : this.makeRandomId(this.comicMinId, this.comicMaxId)
            try {
                this.fetching = 'pending'
                let { data } = await axios.get(`${uriBase}?comic=${this.comicId}`)
                this.comic = data
                this.fetching = 'succeded'
            } catch (error) {
                this.fetching = 'rejected'
                 Swal.fire('Opps', 'Ha ocurrido un error inesperado','error');
            }
        },
        makeRandomId: function(min, max) {
            return Math.floor(Math.random() * (max - min) + min);
        },

    },
    created() {
        this.search();
    }

}
</script>


<style scoped>
.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 100%;
    align-items: center;
    width: 90%;
    box-sizing: border-box;
}

i {
    font-size: 20px;
}
</style>