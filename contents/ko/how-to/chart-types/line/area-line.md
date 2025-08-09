# 영역 차트

영역 차트는 선과 축 사이의 공간을 배경색으로 채워 영역의 크기로 데이터를 표현합니다. 일반적인 선 차트와 비교하여 영역 차트는 더 직관적인 시각적 효과를 가집니다. 시리즈가 적은 시나리오에 특히 적합합니다.

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
      areaStyle: {}
    },
    {
      data: [25, 14, 23, 35, 10],
      type: 'line',
      areaStyle: {
        color: '#ff0',
        opacity: 0.5
      }
    }
  ]
};
```

선 차트의 영역 스타일을 변경하려면 [`areaStyle`](${optionPath}series-line.areaStyle)을 사용해보세요. `'areaStyle'`을 `{}`로 설정하면 기본 타입을 사용합니다: 시리즈의 색상을 사용하여 반투명하게 영역을 채웁니다. 스타일을 변경하려면 `'areaStyle'`의 설정 항목을 재정의해보세요. 예를 들어, 두 번째 시리즈의 색상을 50% 투명도의 노란색으로 변경했습니다.
