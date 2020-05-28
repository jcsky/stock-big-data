<template>
  <div id="chart" style="width: 600px;height:400px;"></div>
</template>
<script>
export default {
  data() {
    return {
      rawData: [
        [
          "2015/12/31",
          "3570.47", // open
          "3539.18", // close
          "-33.69",
          "-0.94%",
          "3538.35", // low
          "3580.6", // high
          "176963664",
          "25403106",
          "-"
        ],
        [
          "2015/12/30",
          "3566.73",
          "3572.88",
          "9.14",
          "0.26%",
          "3538.11",
          "3573.68",
          "187889600",
          "26778766",
          "-"
        ],
        [
          "2015/12/29",
          "3528.4",
          "3563.74",
          "29.96",
          "0.85%",
          "3515.52",
          "3564.17",
          "182551920",
          "25093890",
          "-"
        ],
        [
          "2015/12/28",
          "3635.77",
          "3533.78",
          "-94.13",
          "-2.59%",
          "3533.78",
          "3641.59",
          "269983264",
          "36904280",
          "-"
        ],
        [
          "2015/12/25",
          "3614.05",
          "3627.91",
          "15.43",
          "0.43%",
          "3601.74",
          "3635.26",
          "198451120",
          "27466004",
          "-"
        ],
        [
          "2015/12/24",
          "3631.31",
          "3612.49",
          "-23.6",
          "-0.65%",
          "3572.28",
          "3640.22",
          "227785216",
          "31542126",
          "-"
        ],
        [
          "2015/12/23",
          "3653.28",
          "3636.09",
          "-15.68",
          "-0.43%",
          "3633.03",
          "3684.57",
          "298201792",
          "41990292",
          "-"
        ],
        [
          "2015/12/22",
          "3645.99",
          "3651.77",
          "9.3",
          "0.26%",
          "3616.87",
          "3652.63",
          "261178752",
          "36084604",
          "-"
        ],
        [
          "2015/12/21",
          "3568.58",
          "3642.47",
          "63.51",
          "1.77%",
          "3565.75",
          "3651.06",
          "299849280",
          "39831696",
          "-"
        ],
        [
          "2015/12/18",
          "3574.94",
          "3578.96",
          "-1.03",
          "-0.03%",
          "3568.16",
          "3614.7",
          "273707904",
          "36538580",
          "-"
        ],
        [
          "2015/12/17",
          "3533.63",
          "3580",
          "63.81",
          "1.81%",
          "3533.63",
          "3583.41",
          "283856480",
          "38143960",
          "-"
        ],
        [
          "2015/12/16",
          "3522.09",
          "3516.19",
          "5.83",
          "0.17%",
          "3506.29",
          "3538.69",
          "193482304",
          "26528864",
          "-"
        ],
        [
          "2015/12/15",
          "3518.13",
          "3510.35",
          "-10.31",
          "-0.29%",
          "3496.85",
          "3529.96",
          "200471344",
          "27627494",
          "-"
        ],
        [
          "2015/12/14",
          "3403.51",
          "3520.67",
          "86.09",
          "2.51%",
          "3399.28",
          "3521.78",
          "215374624",
          "27921354",
          "-"
        ],
        [
          "2015/12/11",
          "3441.6",
          "3434.58",
          "-20.91",
          "-0.61%",
          "3410.92",
          "3455.55",
          "182908880",
          "24507642",
          "-"
        ],
        [
          "2015/12/10",
          "3469.81",
          "3455.5",
          "-16.94",
          "-0.49%",
          "3446.27",
          "3503.65",
          "200427520",
          "27949970",
          "-"
        ],
        [
          "2015/12/9",
          "3462.58",
          "3472.44",
          "2.37",
          "0.07%",
          "3454.88",
          "3495.7",
          "195698848",
          "26785488",
          "-"
        ],
        [
          "2015/12/8",
          "3518.65",
          "3470.07",
          "-66.86",
          "-1.89%",
          "3466.79",
          "3518.65",
          "224367312",
          "29782174",
          "-"
        ],
        [
          "2015/12/7",
          "3529.81",
          "3536.93",
          "11.94",
          "0.34%",
          "3506.62",
          "3543.95",
          "208302576",
          "28056158",
          "-"
        ],
        [
          "2015/12/4",
          "3558.15",
          "3524.99",
          "-59.83",
          "-1.67%",
          "3510.41",
          "3568.97",
          "251736416",
          "31976682",
          "-"
        ],
        [
          "2015/12/3",
          "3525.73",
          "3584.82",
          "47.92",
          "1.35%",
          "3517.23",
          "3591.73",
          "281111232",
          "33885908",
          "-"
        ],
        [
          "2015/12/2",
          "3450.28",
          "3536.91",
          "80.6",
          "2.33%",
          "3427.66",
          "3538.85",
          "301491488",
          "36918304",
          "-"
        ],
        [
          "2015/12/1",
          "3442.44",
          "3456.31",
          "10.9",
          "0.32%",
          "3417.54",
          "3483.41",
          "252390752",
          "33025674",
          "-"
        ]
      ]
    };
  },
  methods: {
    calculateMA(dayCount, data) {
      var result = [];
      for (var i = 0, len = data.length; i < len; i++) {
        if (i < dayCount) {
          result.push("-");
          continue;
        }
        var sum = 0;
        for (var j = 0; j < dayCount; j++) {
          sum += data[i - j][1];
        }
        result.push(sum / dayCount);
      }
      return result;
    }
  },
  mounted() {
    console.log(this.rawData);
    var dates = this.rawData.map(function (item) {
        return item[0];
    });

    var data = this.rawData.map(function (item) {
        return [+item[1], +item[2], +item[5], +item[6]];
    });

    let options = {
      backgroundColor: "#21202D",
      legend: {
        data: ["日K", "MA5", "MA10", "MA20", "MA30"],
        inactiveColor: "#777",
        textStyle: {
          color: "#fff"
        }
      },
      tooltip: {
        trigger: "axis",
        axisPointer: {
          animation: false,
          type: "cross",
          lineStyle: {
            color: "#376df4",
            width: 2,
            opacity: 1
          }
        }
      },
      xAxis: {
        type: "category",
        data: dates,
        axisLine: { lineStyle: { color: "#8392A5" } }
      },
      yAxis: {
        scale: true,
        axisLine: { lineStyle: { color: "#8392A5" } },
        splitLine: { show: false }
      },
      grid: {
        bottom: 80
      },
      dataZoom: [
        {
          textStyle: {
            color: "#8392A5"
          },
          handleIcon:
            "M10.7,11.9v-1.3H9.3v1.3c-4.9,0.3-8.8,4.4-8.8,9.4c0,5,3.9,9.1,8.8,9.4v1.3h1.3v-1.3c4.9-0.3,8.8-4.4,8.8-9.4C19.5,16.3,15.6,12.2,10.7,11.9z M13.3,24.4H6.7V23h6.6V24.4z M13.3,19.6H6.7v-1.4h6.6V19.6z",
          handleSize: "80%",
          dataBackground: {
            areaStyle: {
              color: "#8392A5"
            },
            lineStyle: {
              opacity: 0.8,
              color: "#8392A5"
            }
          },
          handleStyle: {
            color: "#fff",
            shadowBlur: 3,
            shadowColor: "rgba(0, 0, 0, 0.6)",
            shadowOffsetX: 2,
            shadowOffsetY: 2
          }
        },
        {
          type: "inside"
        }
      ],
      animation: false,
      series: [
        {
          type: "candlestick",
          name: "日K",
          data: data,
          itemStyle: {
            color: "#FD1050",
            color0: "#0CF49B",
            borderColor: "#FD1050",
            borderColor0: "#0CF49B"
          }
        },
        {
          name: "MA5",
          type: "line",
          data: this.calculateMA(5, data),
          smooth: true,
          showSymbol: false,
          lineStyle: {
            width: 1
          }
        },
        {
          name: "MA10",
          type: "line",
          data: this.calculateMA(10, data),
          smooth: true,
          showSymbol: false,
          lineStyle: {
            width: 1
          }
        },
        {
          name: "MA20",
          type: "line",
          data: this.calculateMA(20, data),
          smooth: true,
          showSymbol: false,
          lineStyle: {
            width: 1
          }
        },
        {
          name: "MA30",
          type: "line",
          data: this.calculateMA(30, data),
          smooth: true,
          showSymbol: false,
          lineStyle: {
            width: 1
          }
        }
      ]
    };
    console.log(options);
    
    this.$echartsInit("chart", options);
  }
};
</script>
