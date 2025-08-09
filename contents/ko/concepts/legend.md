# 범례(Legend)

범례는 서로 다른 색상, 모양 및 텍스트를 사용하여 차트의 내용에 주석을 달고 서로 다른 카테고리를 나타내는데 사용됩니다. 범례를 클릭하면 사용자는 해당 카테고리를 표시하거나 숨길 수 있습니다. 범례는 차트를 이해하는 핵심 요소 중 하나입니다.

## 레이아웃

범례는 항상 차트의 우상단 모서리에 배치됩니다. 동일한 페이지의 모든 범례는 전체 차트 공간의 레이아웃을 고려하여 수평 또는 수직으로 정렬하여 일관성을 유지해야 합니다. 차트의 세로 공간이 적거나 콘텐츠 영역이 혼잡할 때는 범례를 차트 하단에 두는 것도 좋은 선택입니다. 다음은 범례의 몇 가지 레이아웃입니다:

```js live
option = {
  legend: {
    // Try 'horizontal'
    orient: 'vertical',
    right: 10,
    top: 'center'
  },
  dataset: {
    source: [
      ['product', '2015', '2016', '2017'],
      ['Matcha Latte', 43.3, 85.8, 93.7],
      ['Milk Tea', 83.1, 73.4, 55.1],
      ['Cheese Cocoa', 86.4, 65.2, 82.5],
      ['Walnut Brownie', 72.4, 53.9, 39.1]
    ]
  },
  xAxis: { type: 'category' },
  yAxis: {},
  series: [{ type: 'bar' }, { type: 'bar' }, { type: 'bar' }]
};
```

범례가 많은 경우 스크롤 가능한 컨트롤을 사용하세요.

```js
option = {
  legend: {
    type: 'scroll',
    orient: 'vertical',
    right: 10,
    top: 20,
    bottom: 20,
    data: ['Legend A', 'Legend B', 'Legend C' /* ... */, , 'Legend x']
    // ...
  }
  // ...
};
```

## 스타일

어두운 색상 배경의 경우, 배경을 반투명으로 변경하면서 배경 레이어와 텍스트에는 밝은 색상을 사용하세요.

```js
option = {
  legend: {
    data: ['Legend A', 'Legend B', 'Legend C'],
    backgroundColor: '#ccc',
    textStyle: {
      color: '#ccc'
      // ...
    }
    // ...
  }
  // ...
};
```

범례의 색상은 여러 가지 방법으로 디자인할 수 있습니다. 차트마다 범례 스타일이 다를 수 있습니다.

<img max-width="830" width="80%" height="80%" src="images/design/legend/charts_sign_img04.png" />

```js
option = {
  legend: {
    data: ['Legend A', 'Legend B', 'Legend C'],
    icon: 'rect'
    // ...
  }
  // ...
};
```

## 상호작용

환경적 요구에 따라 범례는 상호작용 기능을 지원할 수 있습니다. 범례를 클릭하여 해당 카테고리를 표시하거나 숨길 수 있습니다:

```js
option = {
  legend: {
    data: ['Legend A', 'Legend B', 'Legend C'],
    selected: {
      'Legend A': true,
      'Legend B': true,
      'Legend C': false
    }
    // ...
  }
  // ...
};
```

## 팁

범례는 상황에 따라 사용해야 합니다. 일부 이중 축 차트에는 여러 차트 유형이 포함됩니다. 다양한 종류의 범례 스타일을 구별해야 합니다.

```js
option = {
  legend: {
    data: [
      {
        name: 'Legend A',
        icon: 'rect'
      },
      {
        name: 'Legend B',
        icon: 'circle'
      },
      {
        name: 'Legend C',
        icon: 'pin'
      }
    ]
    //  ...
  },
  series: [
    {
      name: 'Legend A'
      //  ...
    },
    {
      name: 'Legend B'
      //  ...
    },
    {
      name: 'Legend C'
      //  ...
    }
  ]
  //  ...
};
```

차트에 한 종류의 데이터만 있는 경우, 범례 대신 차트 제목을 사용하여 설명하세요.
