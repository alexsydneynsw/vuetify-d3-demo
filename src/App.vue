<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Alex's Vue+Vuetify+D3</span>
        <span class="font-weight-light">TEST</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        href="https://github.com/alexsydneynsw"
        target="_blank"
      >
        <span class="mr-2">My GitHub</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <v-container fluid>
        <v-layout align-start row fill-height>
          <v-flex xs-12>
            <h2>Random data points (updated every 2s)</h2>            
            <responsive-area-chart
            @select="onSelect"
            :ceil="max"
            :data="data"
            class="area-chart" />

            <div class="selected">Selected Value: {{currentValue}}</div>            

            <div>
              <v-text-field v-model:value="itemCount" autofocus label="Random Points Count" />
            </div>
            <div>
              <v-text-field v-model:value="min" label="Min Value" />
            </div>
            <div>
              <v-text-field v-model:value="max" label="Max Value" />
            </div>

          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import ResponsiveAreaChart from './components/ResponsiveAreaChart'
import generateData from './randomData';

export default {
  name: 'App',
  components: {
    ResponsiveAreaChart
  },
  data() {
    return {
      data: [],
      chartWidth: 0,
      currentValue: null,
      itemCount: 25,
      min: 10,
      max: 100,
    };
  },
  mounted() {
    setInterval(() => {
      this.data = generateData(this.itemCount,
        parseInt(this.min, 10),
        parseInt(this.max, 10));
    }, 2000);
  },
  methods: {
    onSelect(value) {
      this.currentValue = value;
    },
  },
}
</script>

<style lang="sass">
.area-chart
  height: 200px

.selected
  margin-top: 40px
  font-weight: bold
</style>
