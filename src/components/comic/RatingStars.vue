<template>
    <fragment>
        <div class="container" v-if="!verified">
            <div class="rating-wrap">
                <div class="center">
                    <fieldset class="rating">
                        <fragment v-for="star in stars" :key="star.id">
                            <input v-model="rate" type="radio" :id="star.id" :name="star.name" :class="star.class" :value="star" />
                            <label :for="star.id" :class="star.class"></label>
                        </fragment>
                    </fieldset>
                </div>
                <section v-if="rate && !verified" class="message-box">
                    <header> ( {{rate.value}} ) {{ rate.message }}</header>
                    <div class="textarea">
                        <textarea placeholder="Escriba algún comentario :)"></textarea>
                    </div>
                    <b-button @click="rating" variant="outline-primary btn-block">Enviar calificación</b-button>
                </section>
            </div>
        </div>
        <div v-else class="verified">
            <i class="fas fa-check-double"></i>
            <strong>¡Felicidades!,</strong> haz enviado la calificación del comic, si quieres seguir calificando, presiona los botones de navegación.
        </div>
    </fragment>
</template>

<script>
import Swal from 'sweetalert2'
import { rates } from './dataSet'

export default {
    name: 'Info',
    props: {
        title: String
    },
    data: () => {
        return {
            rate: null,
            verified: false,
            stars: rates,
        }
    },
    methods: {
        rating: function() {
            Swal.fire({
                title: '¿Está seguro?',
                text: 'Se dispone a calificar el comic',
                icon: 'question',
                confirmButtonText: 'Yeah!',
                cancelButtonText: 'Dejame revisar!',
                showCancelButton: true

            }).then(r => {
                if (r.isConfirmed) {
                    Swal.fire({
                        title: 'Calificado con éxito!',
                        icon: 'success',
                        confirmButtonText: 'Super!',
                    })
                    this.verified = true;
                }
            })
        }
    }
}
</script>

<style>
@import url(https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.css);
:root {
    --my-yelow: #fe7;
}

.container {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
}

.rating-wrap {
    max-width: 900px;
    margin: auto;
    padding: 15px;
    text-align: center;
}

.center {
    margin: auto;
}

#rating-value {
    width: 0px;
    margin: 80px auto 0;
    padding: 10px 5px;
    text-align: center;
    box-shadow: inset 0 0 2px 1px rgba(46, 204, 113, .2);
}

/*styles star rating*/

.rating {
    border: none;
    float: left;
}

label {
    transition: all .3s ease;
}

.rating>input {
    display: none;
}

.rating>label::before {
    content: '\f005';
    font-family: FontAwesome;
    margin: 5px;
    font-size: 3rem;
    display: inline-block;
    cursor: pointer;
}

/*Se le agrega la posición absoluta para que se ubique frente a las estrellas completas*/

.rating>.half::before {
    content: '\f089';
    position: absolute;
    cursor: pointer;
}

/*se ubican todos a la derecha, para que quede 1, 2 ,3 ...*/

.rating>label {
    color: #ddd;
    float: right;
    cursor: pointer;
}

/*1.selector Aplicar estilo a los hermanos del elemento input que se encuentre
    checkeado y este en elmento con la clase rating
*/

.rating>input:checked~label,
.rating:not(:checked)>label:hover,
.rating:not(:checked)>label:hover~label {
    color: #EFD70B;
    text-shadow: 0 0 10px rgba(248, 232, 90, 0.7);
}

.rating>input:checked~label::before {}

.message-box {
    transition: all 2s ease;
}

header {
    width: 100%;
    font-size: 20px;
    color: var(--my-yelow);
    font-weight: 500;
    margin: 5px 0 5px 0;
    text-align: center;
    transition: all 0.2s ease;
}

.textarea textarea {
    height: 100%;
    width: 100%;
    outline: none;
    color: #eee;
    border: 1px solid #333;
    background: #222;
    padding: 10px;
    font-size: 17px;
    resize: none;
}

.verified {
    color: var(--my-yelow);
    padding: 20px;
}
</style>