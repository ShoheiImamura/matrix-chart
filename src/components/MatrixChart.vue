<template>
  <v-container>
    <v-row
      class="text-center"
      justify="center"
      align="center"
      align-content="center"
    >
      <!-- 入力欄 -->
      <v-col cols="12">
        <!-- 縦軸（上）項目 -->
        <v-row class="ma-0 pa-0" align="center">
          <v-col cols="12" class="pa-0">
            <span>X軸項目</span>
          </v-col>
        </v-row>
        <!-- プロット -->
        <v-row
          v-for="i in 9"
          :key="i"
          class="ma-0 pa-0"
          justify="center"
          align="center"
        >
          <v-col
            v-for="j in 9"
            :key="j"
            cols="1"
            class="pa-0"
            justify="center"
            align="center"
          >
            <v-card
              tile
              flat
              hover
              @click="selectPlot(i, j)"
              width="2rem"
              height="2rem"
            >
              <!-- TOP 横ライン -->
              <hr
                v-if="i == 1"
                class="horizontal-top-line pa-0 ma-0"
                z-index="3"
              />

              <!-- 横ライン -->
              <hr
                :class="
                  i == 5 ? 'horizontal-center-line  ' : 'horizontal-line '
                "
              />
              <!-- 縦ライン -->
              <v-divider
                class="vertical-center-line pa-0 ma-0"
                vertical
                :color="j == 5 ? 'black' : ''"
              ></v-divider>
              <!-- 縦ライン -->
              <v-divider
                v-if="j == 1"
                class="vertical-left-line pa-0 ma-0"
                vertical
                color="black"
              ></v-divider>
              <!-- 縦ライン -->
              <v-divider
                v-if="j == 9"
                class="vertical-right-line pa-0 ma-0"
                vertical
                color="black"
              ></v-divider>
              <!-- 要素 -->
              <v-avatar
                v-if="isSelected(i, j)"
                color="red"
                size="12"
                class="ma-0 pa-auto"
                style="vertical-align: middle"
              ></v-avatar>

              <!-- Bottom 横ライン -->
              <hr
                v-if="i == 9"
                class="horizontal-bottom-line pa-0 ma-0"
                z-index="3"
              />
            </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <h6>選択</h6>
        {{ plot }}
      </v-col>
      <v-col cols="12">
        <h6>選択リスト</h6>
        {{ plots }}
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "MatrixChart",

  data: () => ({
    plot: { i: 0, j: 0 },
    plots: [],
  }),

  methods: {
    selectPlot: function (i, j) {
      // 現在の選択
      this.plot = { i: i, j: j, title: "" };

      if (this.isSelected(i, j)) {
        this.omitPlot(i, j);
      } else {
        this.addPlot(i, j);
      }
    },

    addPlot: function (i, j) {
      this.plots.push({ i: i, j: j, title: "" });
    },

    omitPlot: function (i, j) {
      this.plots = this.plots.filter((element) => {
        return element.i != i || element.j != j;
      });
    },

    /**
     * 座標の配列上のindexを返却
     * ※もし無ければ-1を返す
     * @param {*} i
     * @param {*} j
     */
    getPlotIndex: function (i, j) {
      return this.plots.findIndex((element) => {
        return (element.i == i) & (element.j == j);
      });
    },

    /**
     * 選択中かどうか
     */
    isSelected: function (i, j) {
      const plotIndex = this.getPlotIndex(i, j);
      return plotIndex !== -1;
    },
  },
};
</script>

<style scoped>
.circle {
  position: absolute;
  top: 0.5rem;
  left: 0.5rem;
}
.vertical-center-line {
  position: absolute;
  left: 1rem;
}
.vertical-left-line {
  position: absolute;
  left: 0rem;
}
.vertical-right-line {
  position: absolute;
  left: 2rem;
}
.horizontal-center-line {
  position: absolute;
  top: 1rem;
  min-width: 2rem;
  border-top: 1px solid rgb(0, 0, 0);
}
.horizontal-line {
  position: absolute;
  top: 1rem;
  min-width: 2rem;
  border-top: 1px solid rgb(233, 233, 233);
}
.horizontal-top-line {
  position: absolute;
  top: 0rem;
  min-width: 2rem;
  border-top: 0.1px solid black;
}
.horizontal-bottom-line {
  position: absolute;
  top: 2rem;
  min-width: 2rem;
  border-top: 0.1px solid black;
}
</style>