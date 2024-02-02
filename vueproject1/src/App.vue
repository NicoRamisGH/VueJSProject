<template>
    <div>

        <h1>Pago de Propinas</h1>

        <div class="form-group">
            <label for="dividend">Total de propinas: </label>
            <input id="dividend" type="number" v-model="dividend" />
        </div>

        <div class="form-group">
            <label for="divisor">Entre cuantos quieres dividir las Propinas?: </label>
            <input id="divisor" type="number" v-model="divisor" @input="calculateDivision" />
        </div>

        <div class="form-group">
            <label for="selection">Elige el Metodo de Pago: </label>
            <select id="selection" v-model="selection">
                <option value="">-- Seleccione una opcion --</option>
                <option value="Tarjeta de Credito">Tarjeta de Credito</option>
                <option value="Tarjeta de Debito">Tarjeta de Debito</option>
                <option value="Efectivo">Efectivo</option>
            </select>
        </div>

        <div v-if="showResult">
            <h2>Final:</h2>
            <p>Monto por persona: {{ division }}</p>
            <p>Metodo de pago: {{ selection }}</p>
        </div>



        <button @click="saveValues" v-if="isResultDisplayed">Pagar propinas</button>
        <button @click="showValues">Mostrar propinas</button>

        <div v-if="showSavedValues">
            <h2>Valores almacenados:</h2>
            <table>
                <thead >
                    <tr>
                        <th>Propinas:</th>
                        <th>Entre cuantos fue dividida</th>
                        <th>Cantidad para cada uno</th>
                        <th>Metodo de pago</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(dividend, index) in dividends" :key="index">
                        <td>{{ dividend }}</td>
                        <td>{{ divisors[index] }}</td>
                        <td>{{ divisions [index] }}</td>
                        <td>{{ selections[index] }}</td>

                    </tr>
                </tbody>
            </table>
        </div>



    </div>
</template>

<script>

    export default {
        data() {
            return {
                dividend: 0,
                divisor: 0,
                selection: '',
                showResult: false,
                division: 0,
                divisions: [],
                dividends: [],
                divisors: [],
                selections: [],
                showSavedValues: false,
            };
        },

        computed: {
            isResultDisplayed() {
                return this.divisor > 0 && this.selection !== '';
            },
        },

        methods: {
            calculateDivision() {
                if (this.divisor > 0) {
                    this.division = this.dividend / this.divisor;
                    this.showResult = true;
                } else {
                    this.showResult = false;
                }
            },

            saveValues() {
                this.dividends.push(this.dividend);
                this.divisors.push(this.divisor);
                this.selections.push(this.selection);
                this.divisions.push(this.division);

                // Clear the input values
                this.dividend = 0;
                this.divisor = 0;
                this.selection = '';
                this.showResult = false;
                this.division = 0;
            },

            showValues() {
                this.showSavedValues = true;
            },
        },
    };
</script>

<style>

    .container {
        max-width: 600px;
        margin: 0 auto;
    }

    .form-group {
        margin-bottom: 15px;
    }

    label {
        display: block;
        margin-bottom: 5px;
    }

    input,
    select {
        width: 25%;
        padding: 10px;
        box-sizing: border-box;
    }


    button {
        background-color: #4CAF50;
        color: white;
        padding: 10px 20px;
        border: none;
        cursor: pointer;
        text-align: center;
        display: inline-block;
        font-size: 16px;
        margin: 10px 2px;
        transition: 0.3s;
    }

        button:hover {
            background-color: #45a049;
        }

    table {
        border-collapse: collapse;
        width: 100%;
    }

    th, td {
        border: 1px solid black;
        padding: 8px;
        text-align: left;
    }

    th {
        background-color: #45a049;
    }
</style>