<script>
import axios from 'axios';
import { store } from "../store.js"
export default {
    name: "SearchBar",
    data() {
        return {
            store
        }
    },
    methods: {
        searchRestaurants() {
            //inseriamo la tipologia cercata nella home su checkedTypologies 
            store.checkedTypologies.push(store.selectedTypology)
            //redirect to restaurant
            this.$router.push('/restaurants')
        },
    },
    mounted() {
        //typologies
        axios
            .get(store.server + store.typologies_end_point)
            .then((response) => {
                //console.log(response);
                store.typologies = response.data.typologies;

            })
            .catch((err) => {
                console.log(err);
                console.log(err.message);
            });

        const arrow = document.querySelector('.arrow svg')
        const selectEl = document.querySelector('select')
        let isOpen = false
        selectEl.addEventListener('click', () => {
            isOpen = !isOpen
            if (isOpen) {
                arrow.style.rotate = '180deg'
                arrow.style.transition = 'rotate 0.3s ease'
            } else {
                arrow.style.rotate = '0deg'
            }
        })
    }
}
</script>

<template>
    <div class="d-flex gap-4 justify-content-center justify-content-md-start align-items-center">
        <div class="select-wrapper position-relative w-25">
            <select v-model="store.selectedTypology" class="me-4 rounded py-2 w-100">
                <option v-for="typology in store.typologies" :key="typology.id" :value="typology.id">
                    {{ typology.name }}
                </option>
                <!-- Altre opzioni typology... -->
            </select>
            <div class="arrow">
                <svg xmlns="http://www.w3.org/2000/svg" width="31" height="20" viewBox="-5 -4.5 24 24">
                    <path fill="#000000"
                        d="m8 11.243l3.95-3.95a1 1 0 1 1 1.414 1.414l-5.657 5.657a.997.997 0 0 1-1.414 0L.636 8.707A1 1 0 1 1 2.05 7.293L6 11.243V1.657a1 1 0 1 1 2 0v9.586z" />
                </svg>
            </div>
        </div>
        <button class="btn" @click="searchRestaurants">Cerca Ristoranti</button>
    </div>
</template>

<style lang="scss" scoped>
@use '../styles/variables.scss' as *;
@use '../styles/general.scss';

.select-wrapper {
    select {
        background-color: transparent;
        border: 3px solid $d-boo-dark;

    }

    .arrow {
        position: absolute;
        top: 7px;
        right: -14px;
    }

    @media screen and (max-width: 768px) {
        .arrow {
            background-color: $d-boo-orange;
        }
    }
    @media screen and (min-width: 768px) {
        .arrow {
            background-color: $d-boo-background;
        }
    }
}

ul {
    height: 110px;
    overflow-y: scroll;

    ::-webkit-scrollbar {
        display: none;
    }
}

.btn {
    background-color: $d-boo-dark;
    color: $d-boo-light;
    transition: all 0.3s ease;

    &:hover {
        background-color: $d-boo-dark;
        color: $d-boo-orange;
    }
}

a {
    color: $d-boo-dark;
}
</style>