# 데이터의 시각적 매핑(Visual Map of Data)

데이터 시각화는 데이터를 시각적 요소로 매핑하는 과정입니다. 이 과정은 시각적 코딩이라고도 할 수 있으며, 시각적 요소는 시각적 채널이라고도 할 수 있습니다.

Apache ECharts<sup>TM</sup>의 모든 차트 유형에는 이 내장된 매핑 과정이 있습니다. 예를 들어, 선형 차트는 데이터를 _선_으로 매핑하고, 막대 차트는 데이터를 _높이_로 매핑합니다. `graph`, `themeRiver`, `treemap`과 같은 더 복잡한 차트들은 고유한 내장 매핑을 가지고 있습니다.

또한 ECharts는 일반적인 시각적 매핑을 위해 [visualMap 컴포넌트](${optionPath}visualMap)를 제공합니다. `visualMap` 컴포넌트에서 허용되는 시각적 요소는 다음과 같습니다:

- `symbol`, `symbolSize`
- `color`, `opacity`, `colorAlpha`,
- `colorLightness`, `colorSaturation`, `colorHue`

다음으로 `visualMap` 컴포넌트를 사용하는 방법을 소개하겠습니다.

## Data and Dimension

Data are usually stored in [series.data](${optionPath}series.data) in ECharts. Depending on chart types, like list, tree, graph, and so on, the form of data may vary somehow. But they have one common feature, that they are a collection of data items. Every data item contains data value, and other information if needed. Every data value can be a single value (one dimension) or an array (multiple dimensions).

For example, [series.data](${optionPath}series.data) is the most common form, which is a `list`, a common array:

```js
series: {
  data: [
    {
      // every item here is a dataItem
      value: 2323, // this is data value
      itemStyle: {}
    },
    1212, // it can also be a value of dataItem, which is a more common case
    2323, // every data value here is one dimension
    4343,
    3434
  ];
}
```

```js
series: {
  data: [
    {
      // every item here is a dataItem
      value: [3434, 129, 'San Marino'], // this is data value
      itemStyle: {}
    },
    [1212, 5454, 'Vatican'], // it can also be a value of dataItem, which is a more common case
    [2323, 3223, 'Nauru'], // every data value here is three dimension
    [4343, 23, 'Tuvalu'] // If is scatter chart, usually map the first dimension to x axis,
    // the second dimension to y axis,
    // and the third dimension to symbolSize
  ];
}
```

Usually the first one or two dimensions are used for mapping. For example, map the first dimension to x axis, and the second dimension to y axis. If you want to represent more dimensions, `visualMap` is what you need. Most likely, [scatter charts](${optionPath}series-scatter) use radius to represent the third dimension.

## The visualMap Component

visualMap component defines the mapping from _which dimension of data_ to _what visual elements_.

The following two types of visualMap components are supported, identified with [visualMap.type](${optionPath}visualMap.type).

Its structure is defined as:

```js
option = {
  visualMap: [
    // can define multiple visualMap components at the same time
    {
      // the first visualMap component
      type: 'continuous' // defined as continuous visualMap
      // ...
    },
    {
      // the second visualMap component
      type: 'piecewise' // defined as discrete visualMap
      // ...
    }
  ]
  // ...
};
```

## Continuous and Piecewise Visual Mapping Components

The visual mapping component of ECharts is divided into continuous ([visualMapContinuous](${optionPath}visualMap-continuous)) and piecewise ([visualMapPiecewise](${optionPath}visualMap-piecewise)).

Continuous means that the data dimension for visual mapping is a continuous value, while piecewise means that the data is divided into multiple segments or discrete data.

### Continuous Visual Mapping

Continuous type visual mapping can determine the range of visual mapping by specifying the maximum and minimum values.

```js
option = {
  visualMap: [
    {
      type: 'continuous',
      min: 0,
      max: 5000,
      dimension: 3, // the fourth dimension of series.data (i.e. value[3]) is mapped
      seriesIndex: 4, // The fourth series is mapped.
      inRange: {
        // The visual configuration in the selected range
        color: ['blue', '#121122', 'red'], // A list of colors that defines the graph color mapping
        // the minimum value of the data is mapped to 'blue', and
        // the maximum value is mapped to 'red', // the maximum value is mapped to 'red', // the maximum value is mapped to 'red'.
        // The rest is automatically calculated linearly.
        symbolSize: [30, 100] // Defines the mapping range for the graphic size.
        // The minimum value of the data is mapped to 30, // and the maximum value is mapped to 100.
        // The maximum value is mapped to 100.
        // The rest is calculated linearly automatically.
      },
      outOfRange: {
        // Check the out of range visual configuration
        symbolSize: [30, 100]
      }
    }
    // ...
  ]
};
```

where [visualMap.inRange](${optionPath}visualMap.inRange) indicates the style used for data within the data mapping range; while [visualMap.outOfRange](${optionPath}visualMap.outOfRange) specifies the style for data outside the mapping range.

[visualMap.dimension](~visualMap.dimension) specifies which dimension of the data will be visually mapped.

### Piecewise Visual Mapping

The piecewise visual mapping component has three modes.

- Continuous data average segmentation: based on [visualMap-piecewise.splitNumber](${optionPath}visualMap-piecewise.splitNumber) to automatically split the data into pieces equally.
- Continuous data custom segmentation: define the range of each piece based on [visualMap-piecewise.pieces](${optionPath}visualMap-piecewise.pieces).
- Discrete data (categorical data): categories are defined in [visualMap-piecewise.categories](${optionPath}visualMap-piecewise.categories).

To use segmented visual map, you need to set `type` to `'piecewise'` and choose one of the above three configuration items.
