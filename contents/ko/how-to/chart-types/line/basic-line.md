# 기본 선 차트

## 간단한 예제

x축을 `category`, y축을 `value`로 하는 선 차트를 만들기 위해 다음 코드를 사용할 수 있습니다:

```js live
option = {
  xAxis: {
    type: 'category',
    data: ['A', 'B', 'C']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      data: [120, 200, 150],
      type: 'line'
    }
  ]
};
```

이 경우 `xAxis`와 `yAxis` 하에서 축의 타입을 `category`와 `value`로 설정했습니다. 또한 `data`를 통해 x축의 내용을 명시했습니다. `series`에서는 타입을 `line`으로 설정하고 `data`를 통해 세 점의 값을 지정했습니다. 이렇게 해서 간단한 선 차트를 얻었습니다.

> 여기서 `type`은 생략할 수 있습니다. 축의 기본값은 `value`이지만 `xAxis`가 카테고리의 `data`를 지정했기 때문입니다. 이 경우 `ECharts`는 이것이 카테고리 축임을 인식할 수 있습니다.

## 직교 좌표계에서의 선 차트

선 차트를 연속적으로 만들려면 어떻게 구현해야 할까요? 답은 간단합니다. `series`의 `data`에서 모든 값이 두 개의 요소를 포함하는 배열로 표현되기만 하면 됩니다.

```js live
option = {
  xAxis: {},
  yAxis: {},
  series: [
    {
      data: [
        [20, 120],
        [50, 200],
        [40, 50]
      ],
      type: 'line'
    }
  ]
};
```

## 사용자 정의 선 차트

### 선 스타일

선 스타일은 `lineStyle` 설정으로 변경할 수 있습니다. 색상, 선 너비, 다각선 타입, 투명도 등을 지정할 수 있습니다. 자세한 내용은 핸드북 [`series.lineStyle`](${optionPath}series-line.lineStyle)을 참조하세요.

다음은 색상, 선 너비 및 타입을 설정하는 예제입니다.

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
      lineStyle: {
        normal: {
          color: 'green',
          width: 4,
          type: 'dashed'
        }
      }
    }
  ]
};
```

여기서 선 너비를 설정할 때 항목의 선 너비는 변경되지 않습니다. 항목의 선 스타일은 별도로 설정해야 합니다.

### 항목 스타일

항목 스타일은 [`series.itemStyle`](${optionPath}series-line.itemStyle)로 변경할 수 있습니다. `color`, `borderColor`, `borderStyle`, `borderWidth`, `borderType`, `shadowColor`, `opacity` 등이 포함됩니다. `lineType`과 동일하게 작동하므로 더 자세한 논의는 하지 않겠습니다.

## 항목에 값 표시

시리즈에서 항목의 라벨은 [`series.label`](${optionPath}series-line.label)로 지정됩니다. `label` 하의 `show`를 `true`로 변경하면 값이 기본적으로 표시됩니다. 그렇지 않고 [`series.emphasis.label.show`](${optionPath}series-line.emphasis.label.show)가 `true`인 경우, 마우스가 항목 위로 이동할 때만 라벨이 표시됩니다.

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
      label: {
        show: true,
        position: 'bottom',
        textStyle: {
          fontSize: 20
        }
      }
    }
  ]
};
```

## 빈 데이터

`series`에는 빈 데이터가 있습니다. 이는 `0`과는 다릅니다. 빈 요소가 있을 때, 선 차트는 그 점을 통과하지 않고 무시합니다. 즉, 빈 요소는 다음 점들로 연결되지 않습니다.

ECharts에서는 `'-'`를 사용하여 null 데이터를 나타냅니다. 이는 다른 시리즈의 데이터에도 적용됩니다.

```js live
option = {
  xAxis: {
    data: ['A', 'B', 'C', 'D', 'E']
  },
  yAxis: {},
  series: [
    {
      data: [0, 22, '-', 23, 19],
      type: 'line'
    }
  ]
};
```

> 빈 데이터와 0의 차이점을 주의하세요.
