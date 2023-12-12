<style>
.form {
    width: 400px;
    margin: 0 auto;
    padding: 20px;
    background-color: hsl(0, 0%, 5%);
    flex-direction: column;
    border-radius: 10%;
    border: 2px solid #225cc9;



}

input,
textarea {
    width: 93%;
    padding: 10px;
    border: 1px solid #ccc;
    font-size: 16px;
    
}

h1 {
    text-align: center
}

button {
    width: 200px;
    height: 40px;
    background-color: #225cc9;
    color: #ffffff;
    border: none;
    cursor: pointer;
    border-radius: 30%;
}

.error {
    color: red;
    font-weight: bold;
}

.retorno {
    text-align: center;
    display: none;
    margin-top: 20px;
}

.botoes {
    display: flex;
    flex-direction: row;
    margin-top: 20px;
}

.botoes button {
    border: 1px solid #ccc;
    margin-right: 10px;
}

.retorno-dados {
    margin-top: 20px;
    border: 1px solid #ccc;
    text-align: center;
}

.teste {
    text-align: left;
    padding-left: 500px;
}
</style>

<template>
    <div>
        <h1>FORMULÁRIO</h1>
        <div class="form">
            <input type="text" placeholder="Nome completo" v-model="Nome" required>
            <input type="email" placeholder="Endereço de e-mail" v-model="email" required>
            <input type="number" placeholder="Idade" v-model="idade" required>
            <textarea placeholder="Uma breve descrição sobre si mesmo" v-model="descricao"></textarea>

            <div class="botoes">
                <button @click="enviar">Enviar</button>
                <button @click="limpar">Limpar</button>
            </div>
        </div>

        <div class="retorno">
            <h2>Retorno</h2>
            <table>
                <tr>
                    <th>Nome do campo</th>
                    <th>Valor do campo</th>
                </tr>
            </table>
        </div>

        <div class="retorno-dados" v-if="retorno">
            <table class="teste">
                <tr v-for="(valor, campo) in dados" :key="campo">
                    <th>{{ campo }}</th>
                    <td>{{ valor }}</td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            Nome: "",
            email: "",
            idade: "",
            descricao: "",
            retorno: false,
            dados: {}
        };
    },
    methods: {
        enviar() {
            // Validação
            if (!this.email.match(/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/)) {
                alert("O endereço de e-mail é inválido.");
                return;
            }

            if (isNaN(this.idade)) {
                alert("A idade deve ser um número.");
                return;
            }

            if (this.idade < 18 || this.idade > 100) {
                alert("A idade deve estar entre 18 e 100 anos.");
                return;
            }

            // Salvar os dados preenchidos
            this.dados = {
                'Nome Completo: ': this.Nome,
                'Email: ': this.email,
                'Idade:': this.idade,
                'Descrição:': this.descricao
            };

            // Exibir o retorno
            this.retorno = true;
        },
        limpar() {
            this.Nome = "";
            this.email = "";
            this.idade = "";
            this.descricao = "";
        }
    }
}
</script>