# 로즈 차트（나이팅게일 차트）

나이팅게일 차트라고도 불리는 로즈 차트는 일반적으로 같은 반지름이지만 다른 반지름을 가진 섹터로 카테고리를 나타냅니다.

ECharts는 원형 차트의 [`series.roseType`](${optionPath}series-pie.roseType)을 `'area'`로 정의하여 로즈 차트를 구현할 수 있습니다. 다른 모든 설정은 기본 원형 차트와 동일합니다.

```js live
option = {
  series: [
    {
      type: 'pie',
      data: [
        {
          value: 100,
          name: 'A'
        },
        {
          value: 200,
          name: 'B'
        },
        {
          value: 300,
          name: 'C'
        },
        {
          value: 400,
          name: 'D'
        },
        {
          value: 500,
          name: 'E'
        }
      ],
      roseType: 'area'
    }
  ]
};
```
