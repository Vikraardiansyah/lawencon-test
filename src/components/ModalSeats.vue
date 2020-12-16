<template>
  <b-modal
    @hide="handleReset"
    id="modal-seats"
    :hide-footer="true"
    :hide-header="true"
    size="lg"
  >
    <template #default="{hide}">
      <div class="button-close">
        <b-button
          @click="
            hide();
            handleReset();
          "
          variant="transparent"
          ><span>x</span></b-button
        >
      </div>
      <b-container fluid class="pt-5 mb-5">
        <b-row class="justify-content-center">
          <b-col md="9">
            <div class="seat_plan_wrap">
              <b-row>
                <b-col md="6">
                  <h6>Select Seats</h6>
                  <div class="seats">
                    <div class="handle">
                      <img src="../assets/handle.png" alt="handle" />
                    </div>
                    <div class="row1">
                      <ul>
                        <li v-for="row in row1" :key="row">
                          <a
                            :id="row"
                            :title="[row]"
                            @click="handleChange(row)"
                          >
                            <img
                              v-if="rowSelect.includes(row)"
                              src="../assets/fseat.png"
                              alt
                            />

                            <img
                              v-else-if="
                                Object.values(dataSeats)
                                  .map(data => data.seats)
                                  .join()
                                  .includes(row)
                              "
                              src="../assets/bookseat.png"
                              alt
                            />
                            <img v-else src="../assets/bseat.png" alt />
                          </a>
                        </li>
                      </ul>
                      <ul>
                        <li v-for="row in row2" :key="row">
                          <a
                            :id="row"
                            :title="[row]"
                            @click="handleChange(row)"
                          >
                            <img
                              v-if="rowSelect.includes(row)"
                              src="../assets/fseat.png"
                              alt
                            />

                            <img
                              v-else-if="
                                Object.values(dataSeats)
                                  .map(data => data.seats)
                                  .join()
                                  .includes(row)
                              "
                              src="../assets/bookseat.png"
                              alt
                            />
                            <img v-else src="../assets/bseat.png" alt />
                          </a>
                        </li>
                      </ul>
                    </div>
                    <div class="row1">
                      <ul>
                        <li v-for="row in row3" :key="row">
                          <a
                            :id="row"
                            :title="[row]"
                            @click="handleChange(row)"
                          >
                            <img
                              v-if="rowSelect.includes(row)"
                              src="../assets/fseat.png"
                              alt
                            />

                            <img
                              v-else-if="
                                Object.values(dataSeats)
                                  .map(data => data.seats)
                                  .join()
                                  .includes(row)
                              "
                              src="../assets/bookseat.png"
                              alt
                            />
                            <img v-else src="../assets/bseat.png" alt />
                          </a>
                        </li>
                      </ul>
                      <ul>
                        <li v-for="row in row4" :key="row">
                          <a
                            :id="row"
                            :title="[row]"
                            @click="handleChange(row)"
                          >
                            <img
                              v-if="rowSelect.includes(row)"
                              src="../assets/fseat.png"
                              alt
                            />
                            <img
                              v-else-if="
                                Object.values(dataSeats)
                                  .map(data => data.seats)
                                  .join()
                                  .includes(row)
                              "
                              src="../assets/bookseat.png"
                              alt
                            />
                            <img v-else src="../assets/bseat.png" alt />
                          </a>
                        </li>
                      </ul>
                    </div>
                  </div>
                </b-col>
                <b-col md="6">
                  <div class="seat_plan">
                    <table class="table">
                      <thead>
                        <tr>
                          <th>Seats</th>
                          <th>Fare</th>
                          <th>Class</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="(row, index) in rowSelect" :key="index">
                          <td>{{ row }}</td>
                          <td>{{ fare }}</td>
                          <td>Economy</td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                  <div class="total bg-default">
                    <b>Total: {{ total }}</b>
                  </div>
                  <b-row>
                    <b-button
                      class="mt-3 ml-3 btn-block"
                      size="sm"
                      variant="primary"
                    >
                      Confrim
                    </b-button>
                  </b-row>
                </b-col>
              </b-row>
            </div>
          </b-col>
        </b-row>
      </b-container>
    </template>
  </b-modal>
</template>

<script>
export default {
  props: ['fare', 'dataSeats'],
  name: 'ModalSeats',
  data() {
    return {
      rowSelect: [],
      rowBooked: [],
      row1: ['A1', 'B1', 'C1', 'D1', 'E1', 'F1', 'G1', 'H1', 'I1'],
      row2: ['A2', 'B2', 'C2', 'D2', 'E2', 'F2', 'G2', 'H2', 'I2'],
      row3: ['A3', 'B3', 'C3', 'D3', 'E3', 'F3', 'G3', 'H3', 'I3'],
      row4: ['A4', 'B4', 'C4', 'D4', 'E4', 'F4', 'G4', 'H4', 'I4'],
      total: 0,
    };
  },
  methods: {
    handleChange(row) {
      this.rowSelect = [...this.rowSelect, row];
    },
    handleReset() {
      this.rowSelect = [];
    },
  },
};
</script>

<style>
.seat_plan_wrap {
  border: 3px solid coral;
  padding: 40px;
}
.seats {
  width: 201px;
  border: 1px solid #ccc;
  padding: 20px;
  margin: 41px auto;
  /* height: 100%; */
  padding-left: 34px;
  padding-right: 10px;
  float: left;
}
.handle {
  float: left;
  width: 100%;
}
.handle img {
  float: right;
}
.row1 {
  float: left;
  width: 50%;
}

.row1 ul {
  width: 40%;
  float: left;
}

.total {
  margin-top: 10px;
  background: #f7f7f7;
  padding: 7px;
  border: 1px solid #eee;
}

.seat_plan {
  height: 270px;
}
.alert {
  float: left;
}

.button-close {
  display: flex;
  justify-content: flex-end;
}
</style>
