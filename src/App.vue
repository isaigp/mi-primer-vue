    <!--PRACTICA # 1 
    <script setup>
        const name = "vue dinamico";
        const styleColor = "color: blue";
        const arrayColores = ["blue", "red", "peru"];
        const active = true;
        const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];
        const arrayFrutasPrecio = [
            {
                name: "Manzana",
                price: "$1.00",
                description: "Una manzana",
            },
            {
                name: "Pera",
                price: "$2.00",
                description: "Una pera",
            },
            {
                name: "Naranja",
                price: "$3.00",
                description: "Una naranja",
            },
        ];
        const objectFruitsPrice = {
                name: "Manzana",
                price: "$1.00",
                description: "Una manzana",
        };
        const arrayFruitsStock= [
            {
                name: "Manzana",
                price: "$1.00",
                description: "Una manzana",
                stock: 0,
            },
            {
                name: "Pera",
                price: "$2.00",
                description: "Una pera",
                stock: 10,
            },
            {
                name: "Naranja",
                price: "$3.00",
                description: "Una naranja",
                stock: 20,
            },
        ];
        const handleClick = (message) => {
            console.log(message);
        }
    </script>

    <template>
        <h1>Hola {{ name.toUpperCase() }}</h1><br>
        <h1> {{ arrayColores }}</h1> <br>
        <h1 :style="`color: ${arrayColores[2]}`">soy Peru</h1><br>
        <h1 v-if="active === true">Estoy activo v-if</h1>
        <h1 v-else-if="active === false">Estoy inactivo v-else-if</h1>
        <h1 v-else>Estoy indefinido v-else</h1><br>
        <h1 v-show="active">estoy activo v-show</h1><br>

        <ul>
            <span>Recorrer un array </span>
            <li v-for="(fruta, index) in arrayFrutas" :key="index">
            {{index + 1 }} - {{ fruta }}</li>
        </ul> <br>

        <ul>
            <span>Recorrer un array de objetos</span>
            <li v-for="(fruit, index) in arrayFrutasPrecio" :key="index">
                {{ index + 1 }} - {{ fruit.name }} - {{ fruit.price }} - {{ fruit.description }}
            </li>
        </ul><br>

        <ul>
            <span>Recorrer un objeto</span>
            <li v-for="(value, property, index) in objectFruitsPrice" :key="value">
                {{ index + 1 }} - {{ property }} : {{ value }}
            </li>
        </ul><br>

        <ul>
            <span>v-for con v-if</span>
            <template v-for="item in arrayFruitsStock" :key="item.name">
                <li v-if="item.stock > 0">
                    {{ item.name }} - precio: {{ item.price }} - stock: {{ item.stock }}
                </li>
            </template>    
        </ul><br>

        <button v-on:click.right.prevent="handleClick('Oprimiste el boton derecho')">Button Right</button>
        <button @click.middle="handleClick('Oprimiste el boton de en medio')">Button Middle</button>
        <button @click="handleClick('Oprimiste el boton de la izquierda')">Button Left</button> 
    </template>

    <style>
        h1 {
            color:red;
        }
    </style> -->

    <script setup>
        import { ref, computed } from "vue";

        const name = "haz click en los botones";
        const counter = ref(0);
        const arrayRecord = ref([]);

        const addCounter = () => {
            counter.value ++
        }

        const decrementCounter = () => {
            counter.value --
        }

        const resetCounter = () => {
            counter.value = 0
        }

        const updateColor = computed(() => {
            if(counter.value === 0) {
                return 'zero';
            }
            else if(counter.value > 0) {
                return 'positive'
            }
            else {
                return 'negative'
            }
        })

        const recordNumber = () => {
            arrayRecord.value.push(counter.value)
        }

        const disabledAdd = computed(() => {
            if(arrayRecord.value.includes(counter.value)){
                return true;
            } else {
                return false;
            }
        })
    </script>

    <template>
        <div class="container text-center mt-3">
            <h1>Hola, {{ name }}</h1><br>
            <!-- <h2 :class="updateColor"> {{ counter }}</h2> -->

            <h2 :class="counter >= 0 ? 'positive':'negative'"> {{ counter }}</h2>
           <!--  <h2 v-if="counter > 0" style="color:greenyellow"> {{ counter }}</h2>
            <h2 v-else-if="counter === 0" style="color:black"> {{ counter }}</h2>
            <h2 v-else style="color:red"> {{ counter }}</h2><br> -->
            <div class="btn-group">
                <button @click="addCounter" class="btn btn-success" icon="fa fa-trash">Incrementar</button>
                <button @click="decrementCounter" class="btn btn-danger">Disminuir</button>
                <button @click="resetCounter" class="btn btn-secondary">Restaurar</button>
                <button @click="recordNumber()" :disabled="disabledAdd" class="btn btn-primary">Add</button>
            </div>

            <h1 class="mt-4">Numeros Favoritos</h1><br>
            <ul class="list-group">
                <li  class="list-group-item mt-1" v-for="(num, index) in arrayRecord" :key="index">{{ num }}</li>
            </ul>
        </div>
    </template>

    <style>
        h1 {
            color:red;
        }
        .positive {
            color:greenyellow
        }
        .negative {
            color: red
        }
        .zero {
            color: peru
        }
    </style>
