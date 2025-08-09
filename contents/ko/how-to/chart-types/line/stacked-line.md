# 누적 선 차트

[누적 막대 차트](${lang}/how-to/chart-types/bar/stacked-bar)와 마찬가지로, 누적 선 차트는 `series`의 `'stack'`을 사용하여 어떤 시리즈가 함께 누적될지 결정합니다.

```js live
option = {
  xAxis: {
    data: ['A', 'B', 'C', 'D', 'E']
  },
  yAxis: {},
  series: [
    {
      data: [10, 22, 28, 43, 49],
      type: 'line',
      stack: 'x'
    },
    {
      data: [5, 4, 3, 5, 10],
      type: 'line',
      stack: 'x'
    }
  ]
};
```

하지만 명확한 표시 없이는 누적 선 차트인지 일반 선 차트인지 판단하기 어렵습니다. 따라서 누적 선 차트임을 나타내기 위해 선 아래 영역을 색상으로 채우는 것이 권장됩니다.

```js live
option = {
  xAxis: {
    data: ['A', 'B', 'C', 'D', 'E']
  },
  yAxis: {},
  series: [
    {
      data: [10, 22, 28, 43, 49],
      type: 'line',
      stack: 'x',
      areaStyle: {}
    },
    {
      data: [5, 4, 3, 5, 10],
      type: 'line',
      stack: 'x',
      areaStyle: {}
    }
  ]
};
```
