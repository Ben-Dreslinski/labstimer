<template>
    <div>
        <p style="color: pink;">Local Time: {{ time }}</p>

        <div v-for="(time, idx) in regions" :key="time.server">
            <p :style="{ 'color': idealTime(idx) }">{{ time.server }} {{ time.time }}</p>
        </div>
    </div>
  </template>
  
  <script lang="ts">

  interface Region {
    server: string;
    timezone: string;
    time: string;
  }

  import Vue from 'vue';
  
  export default Vue.extend({
    name: 'ClockTimer',
    data: function () {
        return {
            interval: 0,
            time: "",
            regions: [
                {
                    server: 'Africa',
                    timezone: 'Africa/Ndjamena',
                    time: ''
                },
                {
                    server: 'China',
                    timezone: 'Asia/Shanghai',
                    time: ''
                },
                {
                    server: 'Singapore',
                    timezone: 'Asia/Singapore',
                    time: ''
                },
                {
                    server: 'Korea',
                    timezone: 'Asia/Seoul',
                    time: ''
                },
                {
                    server: 'Japan',
                    timezone: 'Asia/Tokyo',
                    time: ''
                },
                {
                    server: 'Europe NORTH',
                    timezone: 'Europe/Berlin',
                    time: ''
                },
                {
                    server: 'Europe CENTRAL',
                    timezone: 'Europe/Prague',
                    time: ''
                },
                {
                    server: 'Europe WEST',
                    timezone: 'Europe/London',
                    time: ''
                },
                {
                    server: 'Europe SOUTH',
                    timezone: 'Europe/Rome',
                    time: ''
                },
                {
                    server: 'Europe EAST',
                    timezone: 'Europe/Minsk',
                    time: ''
                },
                {
                    server: 'Middle East',
                    timezone: 'Asia/Riyadh',
                    time: ''
                },
                {
                    server: 'ME - Dubai',
                    timezone: 'Asia/Dubai',
                    time: ''
                },
                {
                    server: 'Australia',
                    timezone: 'Australia/Melbourne',
                    time: ''
                },
                {
                    server: 'Russia WEST',
                    timezone: 'Asia/Omsk',
                    time: ''
                },
                {
                    server: 'Russia CENTRAL',
                    timezone: 'Asia/Ulaanbaatar',
                    time: ''
                },
                {
                    server: 'Russia EAST',
                    timezone: 'Asia/Yakutsk',
                    time: ''
                },
                {
                    server: 'South America',
                    timezone: 'America/Asuncion',
                    time: ''
                },
                {
                    server: 'SA - Colombia',
                    timezone: 'America/Bogota',
                    time: ''
                },
                {
                    server: 'North America SOUTH EAST',
                    timezone: 'America/New_York',
                    time: ''
                },
                {
                    server: 'North America CENTRAL',
                    timezone: 'America/North_Dakota/New_Salem',
                    time: ''
                },
                {
                    server: 'North America NORTH EAST',
                    timezone: 'America/New_York',
                    time: ''
                },
                {
                    server: 'North America SOUTH',
                    timezone: 'America/Winnipeg',
                    time: ''
                },
                {
                    server: 'North America WEST',
                    timezone: 'America/Los_Angeles',
                    time: ''
                }
            ] as Region[]
        }
    },

    beforeDestroy() {
        clearInterval(this.interval);
    },

    created () {
        this.interval = setInterval(() => {
            this.time = Intl.DateTimeFormat(navigator.language, {
                hour: 'numeric',
                minute: 'numeric',
                second: 'numeric',
                hourCycle: 'h23'
            }).format();

            this.regions.forEach(region => {
                region.time = new Intl.DateTimeFormat(navigator.language, {
                    hour: 'numeric',
                    minute: 'numeric',
                    second: 'numeric',
                    timeZone: region.timezone,
                    hourCycle: 'h23'
                }).format();
            });

            this.regions.sort(this.sortTimes);
        }, 100)
    },

    methods: {
        sortTimes: function (first: Region, second: Region)
        {
            let firstHour = parseInt(first.time.split(":")[0]);
            let secondHour = parseInt(second.time.split(":")[0]);

            let firstDist = Math.abs((firstHour - 3) % 24);
            firstDist = (firstDist > 12) ? 24 - firstDist : firstDist;

            let secondDist = Math.abs((secondHour - 3) % 24);
            secondDist = (secondDist > 12) ? 24 - secondDist : secondDist;

            if (firstDist < secondDist)
            {
                return -1;
            }
            else if (firstDist > secondDist)
            {
                return 1;
            }

            return 0;
        },

        idealTime: function (hour: number)
        {
            if (hour < 3)
            {
                return 'green';
            }
            else if (hour < 6)
            {
                return 'orange';
            }
            else
            {
                return 'red';
            }
        }
    }
  });
  </script>
  
<style>
    .good {
        color: 'green';
    }

    .bad {
        color: 'orange';
    }

    .ugly {
        color: 'red';
    }
</style>
  