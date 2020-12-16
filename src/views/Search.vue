<template>
  <div>
    <Header />
    <search-result-info>
      <b-container class="mt-4">
        <b-row class="justify-content-center">
          <b-col md="10">
            <b-row class="text-center">
              <h6 class="text-capitalize text-center col-md-12 mb-3">
                {{
                  Object.values(datas).length > 0
                    ? Object.values(datas)[
                        Object.values(datas).length - 1
                      ].location.replace('to', '-')
                    : ''
                }}
                On
                {{ date }}
              </h6>
            </b-row>
            <b-row class="mb-3 card card-body">
              <b-row>
                <b-col md="4" class="text-right">
                  <p>
                    <b>Filter By</b>
                  </p>
                </b-col>
                <b-col md="4" class="form-group">
                  <b-form-select size="sm" value>
                    <option value>By Bus</option>
                  </b-form-select>
                </b-col>
                <b-col md="4" class="form-group">
                  <b-form-select size="sm" value>
                    <option value>By Type</option>
                  </b-form-select>
                </b-col>
              </b-row>
            </b-row>
            <b-row class="search-result mb-5 pb-5">
              <table class="table">
                <thead>
                  <tr>
                    <th>Bus Name</th>
                    <th>Dept. Time</th>
                    <th>Coach Type</th>
                    <th>Seats Available</th>
                    <th>Fare</th>
                    <th></th>
                  </tr>
                </thead>
                <tbody>
                  <tr
                    v-for="(data, index) in Object.values(datas)"
                    :key="index"
                  >
                    <td>
                      <h6>{{ data.name }}</h6>
                    </td>
                    <td>{{ data.time }}</td>
                    <td>{{ data.coach_type }}</td>
                    <td>{{ data.seat }}</td>
                    <td>{{ data.fare }}</td>
                    <td>
                      <b-button
                        v-b-modal.modal-seats
                        variant="danger"
                        size="sm"
                        @click="
                          handleSeats(data.fare, Object.keys(datas)[index])
                        "
                        >View Seats</b-button
                      >
                    </td>
                  </tr>
                </tbody>
              </table>
            </b-row>
          </b-col>
        </b-row>
      </b-container>
    </search-result-info>
    <Footer />
    <ModalSeats :fare="fare" :dataSeats="dataSeats" />
  </div>
</template>

<script>
import Header from '@/components/Header';
import Footer from '@/components/Footer';
import ModalSeats from '@/components/ModalSeats';
import moment from 'moment';
import axios from 'axios';

export default {
  props: ['to', 'date'],
  name: 'Search',
  data() {
    return {
      datas: {},
      dataSeats: {},
      fare: '',
    };
  },
  components: {
    Header,
    Footer,
    ModalSeats,
  },
  async mounted() {
    const { data } = await axios.get(
      `https://bdbusticket.firebaseio.com/buses/${this.to}.json`
    );
    if (data === null) {
      this.datas = {};
    } else {
      this.datas = data;
    }

    console.log(Object.keys(this.datas));
  },
  methods: {
    async handleSeats(fare, key) {
      const { data } = await axios.get(
        `https://bdbusticket.firebaseio.com/booking/${moment(this.date)
          .add(7, 'hours')
          .valueOf()}/${key}/seat_booking.json`
      );
      if (data === null) {
        this.dataSeats = [];
      } else {
        this.dataSeats = data;
      }

      this.fare = fare;
      this.$bvModal.show('modal-seats');
    },
  },
};
</script>
