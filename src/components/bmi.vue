<template>
  <div>
    <div class="row col-lg-4 m-auto">
      <div class="card p-0 border-0 rounded-3">
        <div class="card-body">
          <h1 class="card-title">{{ msg }}</h1>
          <p>Oblicz łatwo swój wskaźnik BMI</p>
          <div class="row">
            <div class="col-lg-12">
              <div class="form-floating mb-3">
                <input :class="Validate.weightError ? ' is-invalid' : '' " type="number" min="10" max="200" v-model="weight" class="form-control input-ds" id="weight"  placeholder="Podaj wagę">
                <label for="weight">Waga</label>
              </div>
            </div>
            <div class="col-lg-12">
              <div class="form-floating">
                <input :class="Validate.heightError ? ' is-invalid' : '' " type="number" min="10" max="200" v-model="height" class="form-control input-ds" id="height"  placeholder="Podaj wzrost">
                <label for="height">Wzrost</label>
              </div>
            </div>
          </div>
          <div class="d-flex flex-column py-4">
            <ul class="list-group">
              <li class="list-group-item m-0 animation" :class="bmiCalculation.step == 1 ? 'bg-dark text-white has-decoration' : 'bg-white' ">do <b>18,5</b>	niedowaga</li>
              <li class="list-group-item m-0 animation" :class="bmiCalculation.step == 2 ? 'bg-dark text-white has-decoration' : 'bg-white'"> od  <b>18,5</b> do <b>24,9</b>	waga prawidłowa</li>
              <li class="list-group-item m-0 animation" :class="bmiCalculation.step == 3 ? 'bg-dark text-white has-decoration' : 'bg-white'"> od <b>25</b> do <b>29,9</b>	nadwaga</li>
              <li class="list-group-item m-0 animation" :class="bmiCalculation.step == 4 ? 'bg-dark text-white has-decoration' : 'bg-white'"> powyżej <b>30</b> duża otyłość</li>

            </ul>
          </div>
        </div>
        <div class="card-footer border-0 bg-gradient-dark py-3 text-white d-flex align-items-center justify-content-center" style="height: 92px;">

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

        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'bmi',
  data: function () {
    return {
      height: null,
      classes: null,
      weight: null
    }
  },
  props: {
    msg: String
  },
  computed: {
    Validate: function () {
      var weight = parseInt(this.weight);
      var height = parseInt(this.height);
      var weightError = null;
      var heightError = null;
      if(weight <= 0) {
        weightError = true;
      }
      if(height <= 0) {
        heightError = true;
      }
      return {
        weightError,
        heightError,
      }
    },
    bmiCalculation: function () {
      var weight = parseInt(this.weight);
      var height = parseInt(this.height) / 100;
      var bmi = weight / (height * height)
      if(bmi < 18.5) {
        return {
          massage: 'Niedowaga',
          classes: 'bg-warning',
          value: bmi.toFixed(2),
          step: 1,
        }
      }
      else if (bmi <= 24.9 ) {
        return {
          massage: 'Waga prawidłowa',
          classes: 'bg-success',
          value: bmi.toFixed(2),
          step: 2,
        }
      }
      else if (bmi <= 29.9 ) {
        return {
          massage: 'Nadwaga',
          classes: 'bg-danger',
          value: bmi.toFixed(2),
          step: 3,
        }
      }
      else if (bmi > 30) {
        return {
          massage: 'Otyłość',
          classes: 'bg-danger',
          value: bmi.toFixed(2),
          step: 4,
        }
      }
      return false;
    }
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
