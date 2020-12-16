<template>
  <div>
    <Header />
    <div class="select-bus">
      <div class="overlap" />
      <b-container>
        <b-row class="justify-content-center pb-5 pt-3">
          <b-col md="5" class="block mt-3">
            <b-form @submit.prevent="handleSubmit">
              <b-row>
                <b-col md="6" class="form-group">
                  <label>Leaving From</label>
                  <b-form-select
                    size="sm"
                    v-model="from"
                    @change="handleChange"
                    :options="optionsFrom"
                    required
                  ></b-form-select>
                </b-col>
                <b-col md="6" class="form-group">
                  <label>Going To</label>
                  <b-form-select
                    size="sm"
                    v-model="to"
                    :options="optionsTo"
                    required
                  ></b-form-select>
                </b-col>
                <b-col md="12" class="form-group">
                  <label>Departing On</label>
                  <b-form-datepicker
                    :date-format-options="{
                      year: 'numeric',
                      month: 'numeric',
                      day: 'numeric',
                    }"
                    locale="id"
                    size="sm"
                    v-model="date"
                    required
                  ></b-form-datepicker>
                </b-col>
              </b-row>
              <b-button type="submit" class="btn-search btn-block btn-sm mt-3" v
                ><i class="fas mr-2 fa-search"></i>Search buses</b-button
              >
            </b-form>
          </b-col>
          <b-col md="5" class="slider mt-3">
            <img
              src="../assets/redBus-coupons-offers-1586.png"
              alt="redbus-home"
              class="img-fluid"
            />
          </b-col>
        </b-row>
      </b-container>
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header';
import Footer from '@/components/Footer';
import moment from 'moment';

export default {
  name: 'Home',
  components: {
    Header,
    Footer,
  },
  data() {
    return {
      from: null,
      optionsFrom: [
        { value: null, text: 'Select Palce' },
        { value: 'dhaka', text: 'Dhaka' },
        { value: 'comilla', text: 'Comilla' },
        { value: 'chittagong', text: 'Chittagong' },
      ],
      to: null,
      optionsTo: null,
      date: null,
    };
  },
  methods: {
    handleSubmit() {
      this.$router.push({
        name: 'Search',
        params: {
          to: this.to,
          date: moment(this.date, 'YYYY-MM-DD').format('LL'),
        },
      });
    },
    handleChange(from) {
      switch (from) {
        case 'dhaka':
          this.to = '1109001';
          this.optionsTo = [
            { value: '1109001', text: 'Comilla' },
            { value: '1109002', text: 'Chittagong' },
            { value: '1109004', text: 'KuaKata' },
            { value: '1109005', text: 'Coxs Bazar' },
            { value: '1109006', text: 'Rajshahi' },
          ];
          break;
        case 'comilla':
          this.to = '2209002';
          this.optionsTo = [
            { value: '2209002', text: 'Chittagong' },
            { value: '2209001', text: 'Dhaka' },
            { value: '2209003', text: 'Rajshahi' },
          ];
          break;
        case 'chittagong':
          this.to = '3309003';
          this.optionsTo = [
            { value: '3309003', text: 'Mymensingh' },
            { value: '3309001', text: 'Dhaka' },
            { value: '3309002', text: 'Sylet' },
          ];
          break;
        default:
          this.to = null;
          this.optionsTo = null;
          break;
      }
    },
  },
};
</script>

<style>
.overlap {
  background-color: rgb(178, 190, 195, 0.5);
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 100%;
}
.select-bus {
  background: url(../assets/slider.jpg);
  background-size: cover;
  position: relative;
  min-height: 300px;
}
.block {
  background: #fbfbfb;
  height: 276px;
  padding: 35px;
}
.block li {
  margin: 5px 0;
}
.btn-search {
  background: coral !important;
  border-color: coral !important;
  color: #fff !important;
}

.slider img {
  width: 100%;
  height: 276px;
}
</style>
