<template>
    <div class="container">
        <vs-row style="border:1px solid gray; border-radius: 20px;margin: 20px;">
            <vs-col vs-type="flex" vs-justify="center" vs-align="center" w="4" style="background-color: #fff;height:660px">
            <div class="left" style="padding:10px;font-family: cursive;">
                <header style="font-weight: bolder;">
                    <h3 style="color:#135691 ;">{{ currentTime }}</h3>
                    <p>{{ currentDay }},{{ dayOfMonth }} {{ month }}, {{ year }}</p>
                    <div v-if="greetingMessage === 'Good morning!'">
                        <b-icon-sun-fill />
                        <span style="padding-left: 5px;">{{ greetingMessage }}</span>
                    </div>
                    <div v-else-if="greetingMessage === 'Good afternoon'">
                        <b-icon-sun-fill />
                        <span style="padding-left: 5px;">{{ greetingMessage }}</span>
                    </div>
                    <div v-else>
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-moon-fill" viewBox="0 0 16 16">
                            <path d="M6 .278a.768.768 0 0 1 .08.858 7.208 7.208 0 0 0-.878 3.46c0 4.021 3.278 7.277 7.318 7.277.527 0 1.04-.055 1.533-.16a.787.787 0 0 1 .81.316.733.733 0 0 1-.031.893A8.349 8.349 0 0 1 8.344 16C3.734 16 0 12.286 0 7.71 0 4.266 2.114 1.312 5.124.06A.752.752 0 0 1 6 .278z"/>
                        </svg>
                        <span style="padding-left: 5px;">{{ greetingMessage }}</span>
                    </div> 
                </header>
                <div class="content" style="text-align: center;padding-top: 20px;">
                    <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" fill="currentColor" class="bi bi-brightness-high-fill" viewBox="0 0 16 16">
                            <path d="M12 8a4 4 0 1 1-8 0 4 4 0 0 1 8 0zM8 0a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 0zm0 13a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 13zm8-5a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2a.5.5 0 0 1 .5.5zM3 8a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2A.5.5 0 0 1 3 8zm10.657-5.657a.5.5 0 0 1 0 .707l-1.414 1.415a.5.5 0 1 1-.707-.708l1.414-1.414a.5.5 0 0 1 .707 0zm-9.193 9.193a.5.5 0 0 1 0 .707L3.05 13.657a.5.5 0 0 1-.707-.707l1.414-1.414a.5.5 0 0 1 .707 0zm9.193 2.121a.5.5 0 0 1-.707 0l-1.414-1.414a.5.5 0 0 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .707zM4.464 4.465a.5.5 0 0 1-.707 0L2.343 3.05a.5.5 0 1 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .708z"/>
                    </svg>
                    <p style="font-size: 50px;font-weight: bolder;"> 31.49°C</p>
                    <div class="grid">
                        <vs-row justify="space-between">
                            <vs-col w="2">
                                <div class="max">
                                    <p>Max</p>
                                    <span>32.92°C</span>
                                </div>
                            </vs-col>
                            <vs-col w="2">
                                <div class="min">
                                    <p>Min</p>
                                    <span>27.12°C</span>
                                </div>
                            </vs-col>
                        </vs-row>
                    </div>

                </div>
                <hr>
                <div class="card">
                    <div class="card-body">
                        <h1>Thies</h1>
                        <p>Temperature moyenne: °C</p>
                        <p>
                            <b-icon-sunrise-fill />
                            Sunrise: 6:48AM
                        </p>
                        <p>
                            <b-icon-sunset-fill />
                            Sunser: 07:40PM
                        </p>
                    </div>
                </div>
            </div>
            </vs-col>

            <vs-col vs-type="flex" vs-justify="center" vs-align="center" w="8" >
                <div class="right container" style="background-color: AntiqueWhite;height: 660px;padding: 20px;">
                    <div class="historical">
                        <h3>Historical Data</h3>
                        <div class="grif">
                            <vs-row justify="center" style="text-align: center;">
                                <vs-col :key="index" v-for="col,index in 6" w="2">
                                <p>{{currentTime}}</p>
                                <p><b-icon-cloud-drizzle-fill /></p>
                                <p>31.12°C</p>
                                </vs-col>
                            </vs-row>
                        </div>
                    </div>
                    <div class="para">
                        <h3>Today's Highlight</h3>
                        <div class="container grid" style="text-align: center;">
                            <vs-row>
                                <vs-col w="3" style="margin: 15px;border: 1px solid black;border-radius: 4px; height: 150px; padding: 10px;background-color: #fff">
                                    <h5>Visibility</h5>
                                    <p>19km</p>
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-wind" viewBox="0 0 16 16">
                                        <path d="M12.5 2A2.5 2.5 0 0 0 10 4.5a.5.5 0 0 1-1 0A3.5 3.5 0 1 1 12.5 8H.5a.5.5 0 0 1 0-1h12a2.5 2.5 0 0 0 0-5zm-7 1a1 1 0 0 0-1 1 .5.5 0 0 1-1 0 2 2 0 1 1 2 2h-5a.5.5 0 0 1 0-1h5a1 1 0 0 0 0-2zM0 9.5A.5.5 0 0 1 .5 9h10.042a3 3 0 1 1-3 3 .5.5 0 0 1 1 0 2 2 0 1 0 2-2H.5a.5.5 0 0 1-.5-.5z"/>
                                    </svg>
                                </vs-col>
                                <vs-col w="3" style="margin: 15px;border: 1px solid black;border-radius: 4px; height: 150px; padding: 10px;background-color: #fff">
                                    <h5>Humudity</h5>
                                    <p>50%</p>
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-moisture" viewBox="0 0 16 16">
                                        <path d="M13.5 0a.5.5 0 0 0 0 1H15v2.75h-.5a.5.5 0 0 0 0 1h.5V7.5h-1.5a.5.5 0 0 0 0 1H15v2.75h-.5a.5.5 0 0 0 0 1h.5V15h-1.5a.5.5 0 0 0 0 1h2a.5.5 0 0 0 .5-.5V.5a.5.5 0 0 0-.5-.5h-2zM7 1.5l.364-.343a.5.5 0 0 0-.728 0l-.002.002-.006.007-.022.023-.08.088a28.458 28.458 0 0 0-1.274 1.517c-.769.983-1.714 2.325-2.385 3.727C2.368 7.564 2 8.682 2 9.733 2 12.614 4.212 15 7 15s5-2.386 5-5.267c0-1.05-.368-2.169-.867-3.212-.671-1.402-1.616-2.744-2.385-3.727a28.458 28.458 0 0 0-1.354-1.605l-.022-.023-.006-.007-.002-.001L7 1.5zm0 0-.364-.343L7 1.5zm-.016.766L7 2.247l.016.019c.24.274.572.667.944 1.144.611.781 1.32 1.776 1.901 2.827H4.14c.58-1.051 1.29-2.046 1.9-2.827.373-.477.706-.87.945-1.144zM3 9.733c0-.755.244-1.612.638-2.496h6.724c.395.884.638 1.741.638 2.496C11 12.117 9.182 14 7 14s-4-1.883-4-4.267z"/>
                                    </svg>
                                </vs-col>
                                <vs-col w="3" style="margin: 15px;border: 1px solid black;border-radius: 4px; height: 150px; padding: 10px;background-color: #fff">
                                    <h5>Air Quality</h5>
                                </vs-col>
                            </vs-row>
                        </div>
                    </div>
                    <div class="predection">
                        <h3>Predection</h3>
                        <div class="container grid">
                            <vs-row>
                                <vs-col :key="index" v-for="col,index in 3" w="3" style="margin: 15px;border: 1px solid black;border-radius: 4px; height: 100px;background-color: #fff">
                                Default {{ index + 1 }}
                                </vs-col>
                            </vs-row>
                        </div>
                    </div>
                    <div class="log" >
                        <h3 class="clickable-heading" @click="openWindow" style="cursor: pointer;">Logs</h3>
                    </div>
                </div>
            </vs-col>
        </vs-row>
    
        <div v-if="showWindow" class="window">
            <div class="close"  @click="closeWindow">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-lg" viewBox="0 0 16 16">
                    <path d="M2.146 2.854a.5.5 0 1 1 .708-.708L8 7.293l5.146-5.147a.5.5 0 0 1 .708.708L8.707 8l5.147 5.146a.5.5 0 0 1-.708.708L8 8.707l-5.146 5.147a.5.5 0 0 1-.708-.708L7.293 8 2.146 2.854Z"/>
                </svg>
            </div>
            <vs-table>
                <template #thead>
                    <vs-tr>
                        <vs-th>
                            Name
                        </vs-th>
                        <vs-th>
                            Email
                        </vs-th>
                        <vs-th>
                            Id
                        </vs-th>
                    </vs-tr>
                </template>
            </vs-table>
            <!-- Add your content here -->
        </div>

    </div>
</template>
<script>
import axios from 'axios'
export default{
    name: 'Dash_board',
    data() {
        return {
            showWindow: false,
            tempMoyen:null,
            currentTime: '',
            currentDay: "",
            dayOfMonth: "",
            month: "",
            year: "",
            greetingMessage: "",
        };
    },
    mounted () {
        this.updateTimeAndDate();
        setInterval(this.updateTimeAndDate, 1000);
        axios.get('')
            .then(response => {
                this.TEMP_MOYEN_URL = response.data;
            })
            .catch(error => {
                console.error(error);
                this.TEMP_MOYEN_URL = 'Error fetching data';
            });
        
            axios.get('')
                .then(response => {
                    this.LOGS_URL = response.data;
                })
                .catch(error => {
                    console.error(error);
                    this.LOGS_URL = 'Error fetching data';
                });

    },
    methods: {
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
            this.greetingMessage = "Good morning!";
        } else if (hour >= 12 && hour < 18) {
            this.greetingMessage = "Good afternoon!";
        } else {
            this.greetingMessage = "Good evening!";
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
                console.error('Error getting location:', error);
            }
            );
        } else {
            console.error('Geolocation is not supported by this browser.');
        }
        }
  },
}
</script>
<style scoped>
*{
    box-sizing: border-box;
}
.card{
    background-image: url('~@/assets/thies.jpg');
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
  height: 300px;
  padding: 20px;
  background-color: #fff;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
  border-radius: 5px;
}


</style>