# 부드러운 선 차트

부드러운 선 차트는 기본 선 그래프의 변형입니다. 편안한 시각적 경험을 제공하는 더 좋은 선택입니다. ECharts를 사용할 때 `smooth`를 `true`로 변경하기만 하면 이 효과를 얻을 수 있습니다.

```js live
option = {
  xAxis: {
    data: ['A', 'B', 'C', 'D', 'E']
  },
  yAxis: {},
  series: [
    {
      data: [10, 22, 28, 23, 19],
      type: 'line',
      smooth: true
    }
  ]
};
```
