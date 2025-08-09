# 기본 막대 차트

막대 차트는 불연속 데이터 간의 비교를 나타내는 차트입니다. 막대의 길이는 범주형 데이터와 비례 관계에 있습니다.

막대 차트를 설정하려면 `series`의 `type`을 `'bar'`로 설정해야 합니다.

[[Option]](${optionPath}series-bar)

## 간단한 예제

기본 막대 차트부터 시작해보겠습니다:

```js live
option = {
  xAxis: {
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {},
  series: [
    {
      type: 'bar',
      data: [23, 24, 18, 25, 27, 28, 25]
    }
  ]
};
```

이 경우 x축은 카테고리 타입입니다. 따라서 `'xAxis'`에 대해 해당하는 값들을 정의해야 합니다. 한편, y축의 데이터 타입은 수치형입니다. y축의 범위는 `'series'`의 `data`에 의해 자동으로 생성됩니다.

## 다중 시리즈 막대 차트

시리즈를 사용하여 관련 데이터 그룹을 나타낼 수 있습니다. 같은 차트에서 여러 시리즈를 표시하려면 `series` 아래에 하나 이상의 배열을 추가해야 합니다.

```js live
option = {
  xAxis: {
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {},
  series: [
    {
      type: 'bar',
      data: [23, 24, 18, 25, 27, 28, 25]
    },
    {
      type: 'bar',
      data: [26, 24, 18, 22, 23, 20, 27]
    }
  ]
};
```

## 사용자 정의 막대 차트

### 스타일

['series.itemStyle'](${optionPath}series-bar.itemStyle)을 사용하여 막대 차트의 스타일을 설정하는 것이 좋습니다. 설정 가능한 항목들:

- 열의 색상(`'color'`);
- 열의 테두리 색상(`'borderColor'`), 너비(`'borderWidth'`), 타입(`'borderType'`);
- 열의 테두리 반경(`'barBorderRadius'`);
- 투명도(`'opacity'`);
- 그림자 타입(`'shadowBlur'`, `'shadowColor'`, `'shadowOffsetX'`, `'shadowOffsetY'`)

다음은 예제입니다:

```js live
option = {
  xAxis: {
    data: ['A', 'B', 'C', 'D', 'E']
  },
  yAxis: {},
  series: [
    {
      type: 'bar',
      data: [
        10,
        22,
        28,
        {
          value: 43,
          // 단일 막대의 스타일 지정
          itemStyle: {
            color: '#91cc75',
            shadowColor: '#91cc75',
            borderType: 'dashed',
            opacity: 0.5
          }
        },
        49
      ],
      itemStyle: {
        barBorderRadius: 5,
        borderWidth: 1,
        borderType: 'solid',
        borderColor: '#73c0de',
        shadowColor: '#5470c6',
        shadowBlur: 3
      }
    }
  ]
};
```

이 경우 해당 `series`의 `'itemStyle'`로 막대 차트의 스타일을 정의했습니다. 완전한 설정 항목과 사용법은 설정 항목 매뉴얼을 확인하세요: [`series.itemStyle`](${optionPath}series-bar.itemStyle)。

### 열의 너비와 높이

[`barWidth`](${optionPath}#series-bar.barWidth)를 사용하여 막대의 너비를 변경할 수 있습니다. 예를 들어, 다음 경우의 `'barWidth'`는 `'20%'`로 설정되었습니다. 이는 각 막대의 너비가 카테고리 너비의 20%임을 의미합니다. 모든 시리즈에 5개의 데이터가 있으므로, 20% `'barWidth'`는 전체 x축에 대해 4%를 의미합니다.

```js live
option = {
  xAxis: {
    data: ['A', 'B', 'C', 'D', 'E']
  },
  yAxis: {},
  series: [
    {
      type: 'bar',
      data: [10, 22, 28, 43, 49],
      barWidth: '20%'
    }
  ]
};
```

또한 [`barMaxWidth`](${optionPath}series-bar.barMaxWidth)는 막대의 최대 너비를 제한합니다. 작은 값의 경우 막대의 최소 높이를 선언할 수 있습니다: [`barMinHeight`](${optionPath}series-bar.barMinHeight). 데이터의 해당 높이가 제한보다 작을 때, ECharts는 'barMinHeight'를 대체 높이로 사용합니다.

### 열 간격

열 간격에는 두 가지 종류가 있습니다. 하나는 같은 카테고리 하에서 서로 다른 시리즈 간의 간격입니다: [`barGap`](${optionPath}series-bar.barGap). 다른 하나는 카테고리 간의 간격입니다: [`barCategoryGap`](${optionPath}series-bar.barCategoryGap).

```js live
option = {
  xAxis: {
    data: ['A', 'B', 'C', 'D', 'E']
  },
  yAxis: {},
  series: [
    {
      type: 'bar',
      data: [23, 24, 18, 25, 18],
      barGap: '20%',
      barCategoryGap: '40%'
    },
    {
      type: 'bar',
      data: [12, 14, 9, 9, 11]
    }
  ]
};
```

이 경우 `barGap`은 `'20%'`입니다. 이는 같은 카테고리 하의 막대 간 거리가 막대 너비의 20%임을 의미합니다. 예를 들어, `barCategoryGap`을 `'40%'`로 설정하면, 막대 양쪽의 간격이 카테고리에서 40%의 공간을 차지합니다(열의 너비와 비교하여).

일반적으로 `'barGap'`과 `barCategoryGap`이 설정된 경우 `barWidth`를 명시할 필요가 없습니다. 그래프가 클 때 막대가 너무 넓지 않도록 하려면 `barMaxWidth`를 사용하여 막대의 최대 너비를 제한해보세요.

> 같은 직교 좌표계에서 이 속성은 여러 열 시리즈에 의해 공유됩니다. 그래프에 적용되도록 하려면 시스템의 마지막 막대 차트 시리즈에 이 속성을 설정하세요.

### 막대에 배경색 추가

때로는 막대의 배경색을 변경하고 싶을 수 있습니다. ECharts v4.7.0 이후로 이 기능은 ['showBackground'](${optionPath}series-bar.showBackground)로 활성화하고 ['backgroundStyle'](${optionPath}series-bar.backgroundStyle)로 설정할 수 있습니다.

```js live
option = {
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      data: [120, 200, 150, 80, 70, 110, 130],
      type: 'bar',
      showBackground: true,
      backgroundStyle: {
        color: 'rgba(220, 220, 220, 0.8)'
      }
    }
  ]
};
```
