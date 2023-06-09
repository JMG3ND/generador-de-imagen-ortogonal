<template>
    <div class="ortogonal-cube">
        <div ref="cube" class="ortogonal-cube__cube">
            <div class="ortogonal-cube__face ortogonal-cube__face--up">
                <div v-for="piece, index in image.up" @click="changeColorUp(index)" class="ortogonal-cube__piece"
                    :class="color(piece)">
                </div>
            </div>
            <div class="ortogonal-cube__face ortogonal-cube__face--left">
                <div v-for="piece, index in image.left" @click="changeColorLeft(index)" class="ortogonal-cube__piece"
                    :class="color(piece)">
                </div>
            </div>
            <div class="ortogonal-cube__face ortogonal-cube__face--right">
                <div v-for="piece, index in image.right" @click="changeColorRight(index)" class="ortogonal-cube__piece"
                    :class="color(piece)">
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

//Este componente recebe un objeto con 3 arrays que definen los colores
//de las caras superior (up), izquierda (left), derecha (right)

const image = ref({
    up: [0, 0, 0, 0, 0, 0, 0, 0, 0],
    left: [0, 0, 0, 0, 0, 0, 0, 0, 0],
    right: [0, 0, 0, 0, 0, 0, 0, 0, 0]
});

const changeColorUp = (index) => {
    if (image.value.up[index] < 6) {
        image.value.up[index]++;
    } else {
        image.value.up[index] = 0;
    }
}

const changeColorLeft = (index) => {
    if (image.value.left[index] < 6) {
        image.value.left[index]++;
    } else {
        image.value.left[index] = 0;
    }
}

const changeColorRight = (index) => {
    if (image.value.right[index] < 6) {
        image.value.right[index]++;
    } else {
        image.value.right[index] = 0;
    }
}

//Método que retorna las clases correspondientes al color de la pieza
const color = (element) => {
    switch (element) {
        case 1: return 'ortogonal-cube__piece--white';
        case 2: return 'ortogonal-cube__piece--orange';
        case 3: return 'ortogonal-cube__piece--blue';
        case 4: return 'ortogonal-cube__piece--red';
        case 5: return 'ortogonal-cube__piece--green';
        case 6: return 'ortogonal-cube__piece--yellow';
        default: return '';
    }
}

//Variable de referencia al objeto cubo
const cube = ref(null);

//Lógica que ajusta el tamaño del cubo de la cara Z
const adjustTranslateZ = () => {
    const desplazamiento = window.getComputedStyle(cube.value.children[1]).getPropertyValue("transform");
    const matriz = desplazamiento.match(/matrix3d\(([^)]+)\)/)[1].split(", ");
    const desplazamientoX = parseFloat(matriz[12]);
    cube.value.children[2].style = `transform: translateZ(${-1 * desplazamientoX}px)`;
}

onMounted(() => {
    adjustTranslateZ();
    window.addEventListener('resize', adjustTranslateZ);
});
onUnmounted(() => window.removeEventListener('resize', adjustTranslateZ));
</script>

<style lang="scss">
$red: #ff012d;
$green: #00c400;
$orange: #ff5500;
$blue: #0094c6;
$yellow: #cacc06;
$white: #dfe9e1;

.ortogonal-cube {
    transform-style: preserve-3d;
    display: flex;
    justify-content: center;
    perspective: 300px;
    width: 100%;
    height: 100%;
    max-height: 200px;
    max-width: 200px;

    &__cube {
        transform-style: preserve-3d;
        position: relative;
        height: 100%;
        width: 100%;

        transform: rotateY(50deg) rotateX(337deg) rotateZ(335deg) translate3d(20%, 10%, 0);
    }

    &__face {
        transform-style: preserve-3d;
        position: absolute;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        gap: 3px;
        width: 60%;
        height: 60%;

        &--up {
            transform: translateY(-52%) rotateX(90deg);
        }

        &--left {
            transform: translateX(-52%) rotateY(90deg);
        }

        //El desplazamiento de la cara derecha se hace mediante JS ya que el % es una propiedad de 2 dimenciones y no de 3
        /*&--right { 
            transform: translateZ(35px);
        }*/
    }

    &__piece {
        border: 1px solid black;
        border-radius: 5px;
        width: 100%;
        height: 100%;
        background-color: #8e8e8e;

        &--white {
            background-color: $white;
        }

        &--blue {
            background-color: $blue;
        }

        &--orange {
            background-color: $orange;
        }

        &--yellow {
            background-color: $yellow;
        }

        &--green {
            background-color: $green;
        }

        &--red {
            background-color: $red;
        }
    }
}
</style>