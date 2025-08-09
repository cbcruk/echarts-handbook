# 기본 원형 차트

원형 차트는 주로 전체와 비교한 여러 카테고리의 비율을 보여주는데 사용됩니다. 호도는 각 카테고리의 비율을 나타냅니다.

## 간단한 예제

원형 차트의 설정은 선 차트나 막대 차트와 완전히 동일하지 않습니다. 축을 구성할 필요가 없습니다. 데이터의 이름과 값을 시리즈에서 정의해야 합니다. 기본 원형 차트부터 시작해보겠습니다:

```js live
option = {
  series: [
    {
      type: 'pie',
      data: [
        {
          value: 335,
          name: '직접 방문'
        },
        {
          value: 234,
          name: '연합 광고'
        },
        {
          value: 1548,
          name: '검색 엔진'
        }
      ]
    }
  ]
};
```

언급할 점은 여기서 `value`가 백분율 데이터일 필요가 없다는 것입니다. ECharts는 모든 데이터를 기반으로 원형 차트에서 해당하는 호도를 비례적으로 분배합니다.

## 사용자 정의 원형 차트

### 원형 차트의 반지름

원형 차트의 반지름은 [`series.radius`](${optionPath}series-pie.radius)로 정의할 수 있습니다. 백분율 문자열(`'60%'`)과 절대 픽셀 문자열(`'200'`) 모두 사용할 수 있습니다. 백분율 문자열인 경우, 컸테이너(`'div'`)의 짧은 변과 비례 관계에 있습니다.

```js live
option = {
  series: [
    {
      type: 'pie',
      data: [
        {
          value: 335,
          name: '직접 방문'
        },
        {
          value: 234,
          name: '연합 광고'
        },
        {
          value: 1548,
          name: '검색 엔진'
        }
      ],
      radius: '50%'
    }
  ]
};
```

## 데이터 합계가 0일 때 차트 숨기기

기본적으로 데이터 합계가 0이면 시리즈는 모양을 공평하게 분할합니다. 예를 들어, 모든 4개 시리즈의 값이 0일 때 어떤 모양도 표시하고 싶지 않다면, [`series.stillShowZeroSum`](${optionPath}series-pie.stillShowZeroSum)을 `false`로 정의할 수 있습니다.

```js live
option = {
  series: [
    {
      type: 'pie',
      stillShowZeroSum: false,
      data: [
        {
          value: 0,
          name: '직접 방문'
        },
        {
          value: 0,
          name: '연합 광고'
        },
        {
          value: 0,
          name: '검색 엔진'
        }
      ]
    }
  ]
};
```

라벨도 숨기고 싶다면 [`series.label.show`](${optionPath}series-pie.label.show)도 `false`로 정의하세요.

```js live
option = {
    series: [{
        type: 'pie',
        stillShowZeroSum: false,
        label: {
            show: false
        }
        data: [{
            value: 0,
            name: '직접 방문'
        }, {
            value: 0,
            name: '연합 광고'
        }, {
            value: 0,
            name: '검색 엔진'
        }]
    }]
};
```
