<template>
  <h1>Calendar-Year 2020</h1>
  <div class="row">
    <div class="col-sm-4"></div>
    <div class="col-sm-4">
      <table class="table table-striped table-bordered">
        <thead>
          <tr>
            <th v-for="day in ['Sun','Mon','Tue','Wen','Thu','Fri','Sat']" :key="day">{{day}}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="x in 53" :key="x">
            <td v-for="y in 7" :key="y" :class="{red:inArray(x,y)}">{{getSimpleDateFromXY(x,y)}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { ref } from "vue"; // <-- Use this line if you're in a Vue 3 app
import axios from "axios";

const customHeaders = {
  authorization: `Bearer arc_00009UhD4odlPfyV1qV5rk`,
  "content-type": "application/json",
};

export default {
  components: {},
  setup() {
    const dates = ref([]);
    function setDates(result) {
      result.forEach((obj) => dates.value.push(obj.depart_at));
      //   console.log(dates.value);
    }
    function getSimpleDateFromXY(x, y) {
      var count = (x - 1) * 7 + y - 1;
      var firstDay = new Date(2020, 0, 0).getDay();
      var countFromStart = count - firstDay;
      var time = new Date(
        new Date(2020, 0, 0).getTime() + countFromStart * 1000 * 60 * 60 * 24
      );
      return `${time.getMonth() + 1}/${time.getDate()}`;
    }
    function getDateFromXY(x, y) {
      var count = (x - 1) * 7 + y - 1;
      var firstDay = new Date(2020, 0, 0).getDay();
      var countFromStart = count - firstDay;
      var time = new Date(
        new Date(2020, 0, 0).getTime() + countFromStart * 1000 * 60 * 60 * 24
      );
      return `2020-${time.getMonth() + 1 < 10 ? "0" : ""}${
        time.getMonth() + 1
      }-${time.getDate() < 10 ? "0" : ""}${time.getDate()}`;
    }
    function inArray(x, y) {
      var date = getDateFromXY(x, y);
      return dates.value.indexOf(date) != -1;
    }
    return {
      dates,
      setDates,
      getSimpleDateFromXY,
      getDateFromXY,
      inArray,
    };
  },
  created: function () {
    axios({
      method: "get",
      url: "journey/479",
      baseURL: `http://localhost:8080/v1/`,
      headers: customHeaders,
    })
      .then((res) => {
        var result = res.data.data.items[0].departure;
        this.setDates(result);
      })
      .catch((error) => {
        console.error(error);
      });
  },
};
</script>
<style>
tr td {
  height: 80px;
}
.red {
  background-color: pink;
}
</style>