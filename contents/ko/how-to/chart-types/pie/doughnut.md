# 도너츠 차트

도너츠 차트도 전체와 비교한 값들의 비율을 보여주는데 사용됩니다. 원형 차트와 다른 점은 차트 가운데의 빈 공간을 추가 정보를 제공하는데 사용할 수 있다는 것입니다. 이는 도너츠 차트를 일반적으로 사용되는 차트 유형으로 만듭니다.

## 기본 도너츠 차트

ECharts에서 원형 차트의 반지름은 2개 요소를 가진 배열일 수도 있습니다. 배열의 모든 요소는 문자열 또는 값일 수 있습니다. 첫 번째 요소는 내부 반지름을, 두 번째 요소는 외부 반지름을 나타냅니다.

이러한 관점에서 원형 차트는 내부 반지름이 0인 도너츠 차트의 부분집합입니다.

```js live
option = {
  title: {
    text: '도너츠 차트의 예시',
    left: 'center',
    top: 'center'
  },
  series: [
    {
      type: 'pie',
      data: [
        {
          value: 335,
          name: 'A'
        },
        {
          value: 234,
          name: 'B'
        },
        {
          value: 1548,
          name: 'C'
        }
      ],
      radius: ['40%', '70%']
    }
  ]
};
```

하나의 반지름을 백분율 값의 문자열로, 다른 하나를 값으로 설정하면 일부 해상도에서 내부 반지름이 외부 반지름보다 작을 것입니다. ECharts는 자동으로 더 작은 요소를 내부 반지름으로 선택합니다. 하지만 예상치 못한 결과를 초래하지는 않습니다.

## 강조된 섹터에서 도너츠 가운데에 텍스트 표시

이전 예시는 도너츠 차트 가운데에 고정된 텍스트를 표시하는 방법을 보여주었습니다. 다음 예시는 마우스로 강조된 섹터의 해당 텍스트를 표시하는 방법을 보여줄 것입니다. 일반적인 아이디어는 기본적으로 `label`을 숨기면서 차트 가운데에 `label`을 고정하는 것입니다.

```js live
option = {
  legend: {
    orient: 'vertical',
    x: 'left',
    data: ['A', 'B', 'C', 'D', 'E']
  },
  series: [
    {
      type: 'pie',
      radius: ['50%', '70%'],
      avoidLabelOverlap: false,
      label: {
        show: false,
        position: 'center'
      },
      labelLine: {
        show: false
      },
      emphasis: {
        label: {
          show: true,
          fontSize: '30',
          fontWeight: 'bold'
        }
      },
      data: [
        { value: 335, name: 'A' },
        { value: 310, name: 'B' },
        { value: 234, name: 'C' },
        { value: 135, name: 'D' },
        { value: 1548, name: 'E' }
      ]
    }
  ]
};
```

이 경우 `avoidLabelOverlap`은 ECharts가 격랄을 피하기 위해 라벨의 위치를 조정할지 여부를 제어하는데 사용됩니다. `avoidLabelOverlap`의 기본값은 `true`입니다. 라벨이 가운데에 고정되길 원하므로 `false`로 정의해야 합니다.

따라서 도너츠 차트의 가운데에 강조된 섹터의 `name`이 표시됩니다.
