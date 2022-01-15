<template>
  <div>
    <div class="row col-lg-4 m-auto">
      <div class="card p-0 border-0 rounded-3">
        <div class="card-body">
          <h1 class="card-title">{{ msg }}</h1>
          <p>Oblicz kurs walut</p>
          <div class="row">
            <div class="col-lg-6">
              <div class="form-floating mb-3">
                <input :class="Validate.value ? ' is-invalid' : '' " type="number" min="0" step="0.01" v-model="value" class="form-control input-ds" id="value"  placeholder="Podaj kwotę...">
                <label for="value">Kwota (PLN)</label>
              </div>
            </div>
            <div class="col-lg-6">
              <div class="form-floating mb-3">
                <select :class="Validate.currencyInError ? ' is-invalid' : '' " v-model="currencyOut" class="form-control select" id="currency-in"  placeholder="Wybierz walutę...">
                  <option v-for="currency in currencies" v-bind:value="currency.code" v-bind:key="currency.code" :selected="currencyOut === currency">{{currency.currency }}</option>
                </select>
                <label for="value">Docelowa waluta</label>
              </div>
            </div>

            <div class="col-lg-12">
              <div class="form-floating mb-3">
                <input :class="Validate.result ? ' is-invalid' : '' " type="number" min="0" step="0.01" readonly v-bind:value="exchangeResult" class="form-control input-ds" id="result"  placeholder="Wynik...">
                <label for="value">Wynik ({{ currencyOut }})</label>
              </div>
            </div>
            <!-- <div class="col-lg-6">
              <div class="form-floating mb-3">
                <select :class="Validate.currencyInError ? ' is-invalid' : '' " class="form-control select" id="currency-in"  placeholder="Wybierz walutę...">
                  <option v-for="currency in currencies" v-bind:value="currency.code" v-bind:key="currency.code" :selected="currencyOut === currency">{{currency.currency }}</option>
                </select>
                <label for="value">Waluta</label>
              </div>
            </div> -->
          </div>
        </div>
        <!-- <div class="card-footer border-0 bg-gradient-dark py-3 text-white d-flex align-items-center justify-content-center" style="height: 92px;">

            <div v-if="bmiCalculation.value && !Validate.weightError && !Validate.heightError" class="d-flex flex-row justify-content-between w-100">
              <div class="d-flex flex-column align-items-start">
                <div>
                  Twój wynik:
                </div>
                <div class="fw-bolder fs-4">
                  {{ bmiCalculation.massage }}
                </div>
              </div>
              <div :class="bmiCalculation.classes" class="d-flex align-items-center fs-1 fw-bold rounded-3 px-2">
                {{ bmiCalculation.value }}
              </div>
            </div>
            <div v-else class="fs-5">
              Proszę uzupełnić wartości.
            </div>

        </div> -->
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'exchange',
  data: function () {
    return {
      value: 1,
      currencyIn: 'PLN',
      currencyOut: 'EUR',
      result: null,
      currencies: [],
    }
  },
  props: {
    msg: String
  },
  computed: {
    Validate: function () {
      let valueError = parseInt(this.value) <= 0,
          currencyInError = this.currencies.includes(this.currencyIn),
          currencyOutError = this.currencies.includes(this.currencyOut);

      return {
        valueError,
        currencyInError,
        currencyOutError,
      }
    },
    exchangeResult: function () {
      let found = {... this.currencies.find(currency => currency.code === this.currencyOut)};

      return this.value / found.bid;//found.bid * this.target.value;
    }
  },
  mounted () {
    axios
      .get('http://api.nbp.pl/api/exchangerates/tables/c', null, {
        headers: {
            'Content-Type': 'application/json',
        }
      })
      .then(response => {
        this.currencies = response.data[0].rates;
        console.log(response);
      });  
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-ds {
  border: solid 1px #dfdfdf;
  box-shadow: 0 0 20px rgb(0 0 0 / 5%), 0 0 20px rgb(0 0 0 / 3%);
}
.bg-white {
  background-color: white;
}
.has-decoration:before {
  content: "";
  display: block;
  width: 0;
  height: 0;
  border-top: 8px solid transparent;
  top: 50%;
  transform: translate(0%, -50%);
  border-bottom: 8px solid transparent;
  border-left: 8px solid #ffffff;
  position: absolute;
  left: -1px;
}

.bg-gradient-dark {
  background: #0F2027;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #2C5364, #203A43, #0F2027);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #2C5364, #203A43, #0F2027); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.animation {
  transition: background-color 0.3s ease-in-out;
}
</style>
