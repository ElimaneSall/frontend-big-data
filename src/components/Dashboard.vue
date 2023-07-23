<template>
    <div class="container">
      <vs-row style="border: 1px solid gray; border-radius: 20px; margin: 20px">
        <vs-col
          vs-type="flex"
          vs-justify="center"
          vs-align="center"
          w="4"
          style="background-color: #fff; min-height: 640px"
        >
          <div class="left" style="padding: 10px; font-family: cursive">
            <header style="font-weight: bolder">
              <h3 style="color: #135691">{{ currentTime }}</h3>
              <p>{{ currentDay }},{{ dayOfMonth }} {{ month }}, {{ year }}</p>
              <div v-if="greetingMessage === 'Bonjour!'">
                <b-icon-sun-fill />
                <span style="padding-left: 5px">{{ greetingMessage }}</span>
              </div>
              <div v-else-if="greetingMessage === 'Bon après-midi!'">
                <b-icon-cloud-sun-fill />
                <span style="padding-left: 5px">{{ greetingMessage }}</span>
              </div>
              <div v-else>
                <b-icon-moon-stars-fill />
                <span style="padding-left: 5px">{{ greetingMessage }}</span>
              </div>
            </header>
            <div class="content" style="text-align: center; padding-top: 5px">
              <div class="icon-container" >
                <p v-if="params.temperature >= 25">
                                    <b-icon-sun-fill />
                                  </p>
                                  <p v-else>
                                    <b-icon-cloud-fill />
                                  </p>
              </div>
              <p style="font-size: 50px; font-weight: bolder">
                {{ params.temperature }}°C
              </p>
              <div class="grid">
                <vs-row justify="space-between">
                  <vs-col w="2">
                    <div class="max">
                      <p>Max</p>
                      <span>{{ params.temperatureMax }}°C</span>
                    </div>
                  </vs-col>
                  <vs-col w="2">
                    <div class="min">
                      <p>Min</p>
                      <span>{{ params.temperatureMin }}°C</span>
                    </div>
                  </vs-col>
                </vs-row>
              </div>
            </div>
            <hr />
            <div class="card" style="font-weight: bolder; color: #fff;">
              <div class="card-body">
                <h1>Thiès</h1>
                <p>Température moyenne: {{tempMoyen}}°C</p>
                <p>
                  <b-icon-sunrise-fill />
                  Levée du soleil: {{ params.sunrise.slice(11).split('Z')[0] }}
                  <!-- Sunrise: {{ formatDateTime(new Date(params.sunrise)) }} -->
                </p>
                <p>
                  <b-icon-sunset-fill />
                  Coucher du soleil: {{ params.sunset.slice(11).split('Z')[0] }}
                </p>
              </div>
            </div>
          </div>
        </vs-col>
  
        <vs-col vs-type="flex" vs-justify="center" vs-align="center" w="8">
          <div
            class="right container"
            style="
              background-color: AntiqueWhite;
              min-height: 640px;
              padding: 20px;
            "
          >
            <div class="historical">
              <h3>Températures moyennes par heure</h3>
              <div class="grif">
                  <vs-row justify="center" style="text-align: center;">
                                  <vs-col v-for="item in convertDictToArray()" :key="item.key" w="2">
                                  <p>{{ item.key }}</p>
                                  <p v-if="params.temperature >= 25">
                                    <b-icon-sun-fill />
                                  </p>
                                  <p v-else>
                                    <b-icon-cloud-fill />
                                  </p>
                                  <p>{{ item.value.toFixed(2) }}°C</p>
                                  </vs-col>
                              </vs-row>
              </div>
            </div>
            <div class="para">
              <h3>Données courantes</h3>
              <div class="container grid" style="text-align: center">
                <vs-row>
                  <vs-col
                    w="3"
                    style="
                      margin: 15px;
                      border: 1px solid black;
                      border-radius: 4px;
                      height: 150px;
                      padding: 10px;
                      background-color: #fff;
                    "
                  >
                    <h5>Visibilité</h5>
                    <p>{{ params.visibility }}m</p>
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="16"
                      height="16"
                      fill="currentColor"
                      class="bi bi-wind"
                      viewBox="0 0 16 16"
                    >
                      <path
                        d="M12.5 2A2.5 2.5 0 0 0 10 4.5a.5.5 0 0 1-1 0A3.5 3.5 0 1 1 12.5 8H.5a.5.5 0 0 1 0-1h12a2.5 2.5 0 0 0 0-5zm-7 1a1 1 0 0 0-1 1 .5.5 0 0 1-1 0 2 2 0 1 1 2 2h-5a.5.5 0 0 1 0-1h5a1 1 0 0 0 0-2zM0 9.5A.5.5 0 0 1 .5 9h10.042a3 3 0 1 1-3 3 .5.5 0 0 1 1 0 2 2 0 1 0 2-2H.5a.5.5 0 0 1-.5-.5z"
                      />
                    </svg>
                  </vs-col>
                  <vs-col
                    w="3"
                    style="
                      margin: 15px;
                      border: 1px solid black;
                      border-radius: 4px;
                      height: 150px;
                      padding: 10px;
                      background-color: #fff;
                    "
                  >
                    <h5>Humidité</h5>
                    <p>{{ params.humidity }}%</p>
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="16"
                      height="16"
                      fill="currentColor"
                      class="bi bi-moisture"
                      viewBox="0 0 16 16"
                    >
                      <path
                        d="M13.5 0a.5.5 0 0 0 0 1H15v2.75h-.5a.5.5 0 0 0 0 1h.5V7.5h-1.5a.5.5 0 0 0 0 1H15v2.75h-.5a.5.5 0 0 0 0 1h.5V15h-1.5a.5.5 0 0 0 0 1h2a.5.5 0 0 0 .5-.5V.5a.5.5 0 0 0-.5-.5h-2zM7 1.5l.364-.343a.5.5 0 0 0-.728 0l-.002.002-.006.007-.022.023-.08.088a28.458 28.458 0 0 0-1.274 1.517c-.769.983-1.714 2.325-2.385 3.727C2.368 7.564 2 8.682 2 9.733 2 12.614 4.212 15 7 15s5-2.386 5-5.267c0-1.05-.368-2.169-.867-3.212-.671-1.402-1.616-2.744-2.385-3.727a28.458 28.458 0 0 0-1.354-1.605l-.022-.023-.006-.007-.002-.001L7 1.5zm0 0-.364-.343L7 1.5zm-.016.766L7 2.247l.016.019c.24.274.572.667.944 1.144.611.781 1.32 1.776 1.901 2.827H4.14c.58-1.051 1.29-2.046 1.9-2.827.373-.477.706-.87.945-1.144zM3 9.733c0-.755.244-1.612.638-2.496h6.724c.395.884.638 1.741.638 2.496C11 12.117 9.182 14 7 14s-4-1.883-4-4.267z"
                      />
                    </svg>
                  </vs-col>
                  <vs-col
                    w="3"
                    style="
                      margin: 15px;
                      border: 1px solid black;
                      border-radius: 4px;
                      height: 150px;
                      padding: 10px;
                      background-color: #fff;
                    "
                  >
                    <h5>Vitesse du vent</h5>
                    <p>{{ params.windSpeed }} km/h</p>
                  </vs-col>
                </vs-row>
              </div>
            </div>
            <div class="predection">
              <h3>Prédiction des 3 prochaines heures</h3>
              <div class="container grid">
                <vs-row>
                  <vs-col
                    :key="index"
                    v-for="(col, index) in predection.next_3_hours_temp"
                    w="3"
                    style="
                      margin: 15px;
                      border: 1px solid black;
                      border-radius: 4px;
                      height: 120px;
                      background-color: #fff;
                      text-align: center;
                    "
                  >
                    <p>{{ col.datetime.split(' ')[1] }}</p>
                    <p v-if="params.temperature >= 25">
                                    <b-icon-sun-fill />
                                  </p>
                                  <p v-else>
                                    <b-icon-cloud-fill />
                                  </p>
                    <p>{{ col.predicted_temp.toFixed(2) }}°C</p>
                  </vs-col>
                </vs-row>
              </div>
            </div>
            <div class="log">
              <h3
                class="clickable-heading"
                @click="openWindow"
                style="cursor: pointer"
              >
                Journalisation
              </h3>
            </div>
          </div>
        </vs-col>
      </vs-row>
  
      <div v-if="showWindow" class="window">
        <div class="close" @click="closeWindow">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="16"
            height="16"
            fill="currentColor"
            class="bi bi-x-lg"
            viewBox="0 0 16 16"
          >
            <path
              d="M2.146 2.854a.5.5 0 1 1 .708-.708L8 7.293l5.146-5.147a.5.5 0 0 1 .708.708L8.707 8l5.147 5.146a.5.5 0 0 1-.708.708L8 8.707l-5.146 5.147a.5.5 0 0 1-.708-.708L7.293 8 2.146 2.854Z"
            />
          </svg>
        </div>
        <vs-table>
          <template #thead>
            <vs-tr>
              <vs-th> Date </vs-th>
              <vs-th> Description </vs-th>
              <vs-th> Type </vs-th>
              <vs-th> Status </vs-th>
            </vs-tr>
          </template>
  
          <template #tbody>
            <vs-tr :key="i" v-for="(tr, i) in displayedLogs" :data="tr" :class="getClassByType(tr.type)">
              <vs-td>
                {{ tr.dateLog.split('T')[0] }}  {{ tr.dateLog.split('T')[1].split('Z')[0] }}
              </vs-td>
              <vs-td>
                {{ tr.descript }}
              </vs-td>
              <vs-td>
                {{ tr.type }}
              </vs-td>
              <vs-td>
                {{ tr.status }}
              </vs-td>
            </vs-tr>
          </template></vs-table>
          <vs-pagination v-model="currentPage" :length="totalPages" @change="onChangePage" />
      </div>
    </div>
</template>
  <script>
  import axios from "axios";
//   import { format } from 'date-fns';
// import frLocale from 'date-fns/locale/fr';
  export default {
    name: "Dash_board",
    props: {
      itemsPerPage: {
        type: Number,
        default: 10,
      },
    },
    data() {
      return {
        currentPage: 1,
        logs:null,
        predection: null,
        params: null,
        historicals:null,
        showWindow: false,
        tempMoyen: null,
        currentTime: "",
        currentDay: "",
        dayOfMonth: "",
        month: "",
        year: "",
        greetingMessage: "",
      };
    },
    computed: {
      totalPages() {
        return Math.ceil(this.logs.length / this.itemsPerPage);
      },
      displayedLogs() {
        const startIndex = (this.currentPage - 1) * this.itemsPerPage;
        const endIndex = startIndex + this.itemsPerPage;
        return this.logs.slice(startIndex, endIndex);
      },
    },
    mounted() {
      this.updateTimeAndDate();
      setInterval(this.updateTimeAndDate, 1000);
      axios
        .get("http://localhost/predict-next-3-hours-temp")
        .then((response) => {
          this.predection = response.data;
        })
        .catch((error) => {
          console.error(error);
          this.predection = "Error fetching data";
        });
  
      axios
        .get(
          "http://localhost:8080/backend-weather-1.0-SNAPSHOT/api/meteo/meamTemperatureToday"
        )
        .then((response) => {
          this.tempMoyen = response.data;
        })
        .catch((error) => {
          console.error(error);
          this.tempMoyen = "Error fetching data";
        });
        axios
        .get(
          "http://localhost:8080/backend-weather-1.0-SNAPSHOT/api/meteo/meamTemperaturePerHour"
        )
        .then((response) => {
          this.historicals = response.data;
        })
        .catch((error) => {
          console.error(error);
          this.historicals = "Error fetching data";
        });
      axios
        .get(
          "http://localhost:8080/backend-weather-1.0-SNAPSHOT/api/meteo/lastData"
        )
        .then((response) => {
          this.params = response.data;
        })
        .catch((error) => {
          console.error(error);
          this.params = "Error fetching data";
        });
      axios
        .get("http://localhost:8080/backend-weather-1.0-SNAPSHOT/api/log")
        .then((response) => {
          this.logs = response.data;
        })
        .catch((error) => {
          console.error(error);
          this.logs = "Error fetching data";
        });
    },
    methods: {
      getTemperatureIcon() {
    if (this.params.temperature >= 23) {
      return 'sun-icon'; // Use the sun icon class for high temperatures
    } else {
      return 'moon-icon'; // Use the moon icon class for low temperatures
    }
  },
  getClassByType(type) {
      // Define your class mappings here
      // For example, you can use a switch statement or an object mapping
      switch (type) {
        case "absence":
          return "absence";
        case "retard":
          return "retard";
        case "normal":
          return "normal";
        // Add more cases as needed for other types
        default:
          return ""; // Return an empty string for types with no specific color
      }
    },
      convertDictToArray() {
        const arr = Object.entries(this.historicals).map(([key, value]) => ({ key, value }));
        return arr.reverse();
      },
      onChangePage(page) {
        this.currentPage = page;
      },
      openWindow() {
        this.showWindow = true;
      },
      closeWindow() {
        this.showWindow = false;
      },
      updateTimeAndDate() {
        const now = new Date();
        // Format the time to HH:mm:ss
        const timeString = now.toLocaleTimeString([], {
          hour: "2-digit",
          minute: "2-digit",
        });
        this.currentTime = timeString;
        // Get the day of the week and format it to the full weekday name
        const dayString = now.toLocaleDateString([], { weekday: "long" });
        this.currentDay = dayString;
  
        // Get the day of the month
        const dayOfMonth = now.getDate();
        this.dayOfMonth = dayOfMonth;
  
        // Get the month and format it to the full month name
        const monthString = now.toLocaleDateString([], { month: "long" });
        this.month = monthString;
  
        // Get the year
        const year = now.getFullYear();
        this.year = year;
        const hour = now.getHours();
        if (hour >= 5 && hour < 12) {
          this.greetingMessage = "Bonjour!";
        } else if (hour >= 12 && hour < 18) {
          this.greetingMessage = "Bon après-midi!";
        } else {
          this.greetingMessage = "Bonsoir!";
        }
      },
      updateLocation() {
        if (navigator.geolocation) {
          navigator.geolocation.getCurrentPosition(
            (position) => {
              this.latitude = position.coords.latitude;
              this.longitude = position.coords.longitude;
            },
            (error) => {
              console.error("Error getting location:", error);
            }
          );
        } else {
          console.error("Geolocation is not supported by this browser.");
        }
      },
    },
  };
  </script>
  <style scoped>
  * {
    box-sizing: border-box;
  }
  .card {
    background-image: url("~@/assets/thies.jpg");
    border-radius: 5px;
    
  }
  
  .clickable-heading {
    cursor: pointer;
    padding: 10px;
    background-color: #f0f0f0;
    border: 1px solid #ddd;
    border-radius: 5px;
    text-align: center;
  }
  
  .window {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 800px;
    min-height: 300px;
    padding: 20px;
    background-color: #fff;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    border-radius: 5px;
  }
  .absence {
  background-color: #ff0000; /* Red */
}

.retard {
  background-color: #00ff00; /* Green */
}

.normal {
  background-color: #f0f0f0; /* Blue */
}
.icon-container {
  font-size: 100px; /* Adjust the font size to change the icon size */
}
  </style>