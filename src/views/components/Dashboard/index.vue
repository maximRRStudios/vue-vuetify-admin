<template>
  <div class="grey lighten-3">
    <github-corner class="github-corner"/>
    <v-container fluid grid-list-md text-xs-center>
      <panel-group @handleSetLineChartData="handleSetLineChartData"/>
      <v-layout row wrap>
        <v-flex d-flex xs12>
          <d-widget header-title="Line Chart">
            <option-chart height="350px" width="100%" :chart-data="getChartOption('line')"/>
          </d-widget>
        </v-flex>
      </v-layout>
      <v-layout row wrap>
        <v-flex xs12 sm6 md4>
          <d-widget header-title="Raddar Chart">
            <option-chart height="300px" width="100%" :chart-data="getChartOption('raddar')"/>
          </d-widget>
        </v-flex>
        <v-flex xs12 sm6 md4>
          <d-widget header-title="Pie Chart">
            <option-chart height="300px" width="100%" :chart-data="getChartOption('pie')"/>
          </d-widget>
        </v-flex>
        <v-flex xs12 sm6 md4>
          <d-widget header-title="Bar Chart">
            <option-chart height="300px" width="100%" :chart-data="getChartOption('bar')"/>
          </d-widget>
        </v-flex>
      </v-layout>
      <v-layout row wrap>
        <v-flex lg7 sm12 xs12>
          <d-widget header-title="Projects">
            <plain-table/>
          </d-widget>
        </v-flex>
        <v-flex lg5 sm12 xs12>
          <d-widget header-title="Orders">
            <plain-table-order/>
          </d-widget>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
import {
  lineChartData,
  getLineChartOption,
  getRaddarChartOption,
  getPieChartOption,
  getBarChartOption
} from '@/api/mock';
import * as Activity from '@/api/mock_activity';

import GithubCorner from '@/views/components/Dashboard/GithubCorner.vue';
import PanelGroup from '@/views/components/Dashboard/PanelGroup.vue';
import OptionChart from '@/views/components/Dashboard/OptionChart.vue';
import DWidget from '@/views/components/Dashboard/DWidget.vue';
import PlainTable from '@/views/components/Dashboard/PlainTable.vue';
import PlainTableOrder from '@/views/components/Dashboard/PlainTableOrder.vue';

export default {
  name: 'Dashboard',
  components: {
    GithubCorner,
    PanelGroup,
    OptionChart,
    PlainTable,
    PlainTableOrder,
    DWidget
  },
  data: () => ({
    lineChartData: lineChartData.newVisitis
  }),
  methods: {
    handleSetLineChartData(type) {
      this.lineChartData = lineChartData[type];
    },
    getChartOption(option) {
      switch (option) {
        case 'line':
          return getLineChartOption(this.lineChartData);
        case 'raddar':
          return getRaddarChartOption({ animationDuration: 3000 });
        case 'pie':
          return getPieChartOption();
        case 'bar':
          return getBarChartOption({ animationDuration: 6000 });
        default:
          return {};
      }
    }
  },
  computed: {
    activity() {
      return Activity.default.getActivity();
    }
  }
};
</script>
