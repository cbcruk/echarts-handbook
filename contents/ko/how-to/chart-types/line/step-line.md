# 계단 선 차트

일반적인 선 차트는 두 점을 직선으로 직접 연결하는 반면, 계단 선 차트(사각파 차트라고도 함)는 수평선과 수직선만을 사용하여 인근한 항목들을 연결합니다. 일반적인 선 차트와 비교하여 계단 선 차트는 분석 데이터의 급격한 변화를 두드러지게 보여줍니다.

ECharts에서 `step`은 계단 선 차트의 연결 타입을 특성화하는데 사용됩니다. 세 개의 사용 가능한 값이 있습니다: `'start'`, `'end'`, `'middle'`. 항목 A와 B에 대해 이 값들은 모서리가 A, B, A와 B 사이의 중간지점에서 발생하는 것에 해당합니다.

```js live
option = {
  legend: {},
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      name: '시작 계단',
      type: 'line',
      step: 'start',
      data: [120, 132, 101, 134, 90, 230, 210]
    },
    {
      name: '중간 계단',
      type: 'line',
      step: 'middle',
      data: [220, 282, 201, 234, 290, 430, 410]
    },
    {
      name: '끝 계단',
      type: 'line',
      step: 'end',
      data: [450, 432, 401, 454, 590, 530, 510]
    }
  ]
};
```

> 세 개의 다른 타입 간의 선 차이에 주목하세요.
