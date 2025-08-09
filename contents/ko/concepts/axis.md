# 축(Axis)

데카르트 좌표계에서 사용되는 x/y축입니다.

## x축, y축

x축과 y축 모두 축 선, 눈금, 라벨 및 제목을 포함합니다. 일부 차트는 그리드를 사용하여 데이터 확인과 계산을 지원합니다.

<img max-width="830" width="100%" height="100%"
src="images/design/axis/charts_axis_img02.jpg">
</img>

일반적인 2D 좌표계는 x축과 y축을 가집니다. X축은 일반적으로 하단에, y축은 좌측에 위치합니다. 설정은 아래와 같습니다:

```js
option = {
  xAxis: {
    // ...
  },
  yAxis: {
    // ...
  }
  // ...
};
```

x축은 보통 데이터를 관찰하는 관점이라고도 할 수 있는 카테고리의 수를 선언하는데 사용됩니다: "판매 시간", "판매 위치", "제품명" 등. y축은 일반적으로 카테고리의 수치 값을 나타내는데 사용됩니다. 이 데이터는 "판매 수량", "판매 가격"과 같이 특정 유형의 데이터나 분석해야 하는 지표의 정량적 값을 검사하는데 사용됩니다.

```js
option = {
  xAxis: {
    type: 'time',
    name: '판매 시간'
    // ...
  },
  yAxis: {
    type: 'value',
    name: '판매 수량'
    // ...
  }
  // ...
};
```

x축의 범위가 클 때, 줌 기능을 사용하여 차트의 일부 데이터만 표시할 수 있습니다.

```js
option = {
  xAxis: {
    type: 'time',
    name: '판매 시간'
    // ...
  },
  yAxis: {
    type: 'value',
    name: '판매 수량'
    // ...
  },
  dataZoom: []
  // ...
};
```

2차원 데이터에는 두 개 이상의 축이 있을 수 있습니다. ECharts에서는 보통 두 개의 x축 또는 y축이 동시에 있습니다. 같은 위치에서 축의 중첩을 방지하기 위해 [offset](${optionPath}xAxis.offset) 설정을 변경할 수 있습니다. X축은 위쪽과 아래쪽에, y축은 좌측과 우측에 표시될 수 있습니다.

```js
option = {
  xAxis: {
    type: 'time',
    name: '판매 시간'
    // ...
  },
  yAxis: [
    {
      type: 'value',
      name: '판매 수량'
      // ...
    },
    {
      type: 'value',
      name: '판매 가격'
      // ...
    }
  ]
  // ...
};
```

## 축 선(Axis Line)

ECharts는 [axisLine](${optionPath}xAxis.axisLine)의 설정을 제공합니다. 양쪽 끝의 화살표나 축의 스타일 등 필요에 따라 설정을 변경할 수 있습니다.

```js
option = {
  xAxis: {
    axisLine: {
      symbol: 'arrow',
      lineStyle: {
        type: 'dashed'
        // ...
      }
    }
    // ...
  },
  yAxis: {
    axisLine: {
      symbol: 'arrow',
      lineStyle: {
        type: 'dashed'
        // ...
      }
    }
  }
  // ...
};
```

## 눈금(Tick)

ECharts는 [axisTick](${optionPath}xAxis.axisTick) 설정을 제공합니다. 눈금의 길이와 스타일 등 필요에 따라 설정을 변경할 수 있습니다.

```js
option = {
  xAxis: {
    axisTick: {
      length: 6,
      lineStyle: {
        type: 'dashed'
        // ...
      }
    }
    // ...
  },
  yAxis: {
    axisTick: {
      length: 6,
      lineStyle: {
        type: 'dashed'
        // ...
      }
    }
  }
  // ...
};
```

## 라벨(Label)

ECharts는 [axisLabel](${optionPath}xAxis.axisLabel) 설정을 제공합니다. 텍스트 정렬이나 사용자 정의 라벨 내용 등 필요에 따라 설정을 변경할 수 있습니다.

```js
option = {
  xAxis: {
    axisLabel: {
      formatter: '{value} kg',
      align: 'center'
      // ...
    }
    // ...
  },
  yAxis: {
    axisLabel: {
      formatter: '{value} ¥',
      align: 'center'
      // ...
    }
  }
  // ...
};
```

## 예제

왼쪽의 y축은 도쿄의 월 평균 기온을, 오른쪽의 y축은 도쿄의 강수량을 나타냅니다. x축은 시간을 나타냅니다. 이는 평균 기온과 강수량 사이의 트렌드와 관계를 보여줍니다.

```js live
option = {
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'cross' }
  },
  legend: {},
  xAxis: [
    {
      type: 'category',
      axisTick: {
        alignWithLabel: true
      },
      axisLabel: {
        rotate: 30
      },
      data: [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'October',
        'November',
        'December'
      ]
    }
  ],
  yAxis: [
    {
      type: 'value',
      name: 'Precipitation',
      min: 0,
      max: 250,
      position: 'right',
      axisLabel: {
        formatter: '{value} ml'
      }
    },
    {
      type: 'value',
      name: 'Temperature',
      min: 0,
      max: 25,
      position: 'left',
      axisLabel: {
        formatter: '{value} °C'
      }
    }
  ],
  series: [
    {
      name: 'Precipitation',
      type: 'bar',
      yAxisIndex: 0,
      data: [6, 32, 70, 86, 68.7, 100.7, 125.6, 112.2, 78.7, 48.8, 36.0, 19.3]
    },
    {
      name: 'Temperature',
      type: 'line',
      smooth: true,
      yAxisIndex: 1,
      data: [
        6.0,
        10.2,
        10.3,
        11.5,
        10.3,
        13.2,
        14.3,
        16.4,
        18.0,
        16.5,
        12.0,
        5.2
      ]
    }
  ]
};
```

이것은 축 설정 사용법에 대한 간결한 소개입니다. 자세한 내용은 [공식 웹사이트](${optionPath}xAxis)에서 확인하세요.
