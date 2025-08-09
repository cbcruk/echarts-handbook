# 비동기 데이터 로드 및 동적 업데이트

## 비동기 로드

[시작 가이드 예제](${lang}/get-started)의 데이터는 `setOption`을 사용하여 직접 업데이트됩니다. 하지만 많은 경우 데이터는 비동기 로드로 자주 채워져야 합니다. `ECharts`는 비동기 로드를 간단한 방닝으로 구현할 수 있습니다. jQuery와 같은 함수를 통해 데이터를 비동기로 가져오고 차트가 초기화된 후 `setOption`을 사용하여 데이터와 설정을 채울 수 있습니다.

```js
var myChart = echarts.init(document.getElementById('main'));

$.get('data.json').done(function(data) {
  // Structure of data:
  // {
  //     categories: ["Shirt","Wool sweater","Chiffon shirt","Pants","High-heeled shoes","socks"],
  //     values: [5, 20, 36, 10, 10, 20]
  // }
  myChart.setOption({
    title: {
      text: '비동기 로드 예제'
    },
    tooltip: {},
    legend: {},
    xAxis: {
      data: data.categories
    },
    yAxis: {},
    series: [
      {
        name: '판매',
        type: 'bar',
        data: data.values
      }
    ]
  });
});
```

Or display empty axes with all styles defined before fill in the data:

```js
var myChart = echarts.init(document.getElementById('main'));
// Show title, legends and empty axes
myChart.setOption({
  title: {
    text: '비동기 로드 예제'
  },
  tooltip: {},
  legend: {
    data: ['Sales']
  },
  xAxis: {
    data: []
  },
  yAxis: {},
  series: [
    {
      name: 'Sales',
      type: 'bar',
      data: []
    }
  ]
});

// Asynchronous Data Loading
$.get('data.json').done(function(data) {
  // Fill in the data
  myChart.setOption({
    xAxis: {
      data: data.categories
    },
    series: [
      {
        // Find series by name
        name: '판매',
        data: data.data
      }
    ]
  });
});
```

For example:

<md-example src="doc-example/tutorial-async"></md-example>

You need to use `name` to "navigate" ECharts when updating data. In the previous example, the chart can update normally depending on the order of series, but we recommend you to add the `name` data while updating data.

## loading Animation

When it takes a long time to load the data, the user is facing the empty chart with only axes will wonder if there is a bug.

ECharts have a simple loading animation by default. You can call [showLoading](${mainSitePath}/api.html#echartsInstance.showLoading) to display. When the data loading was completed, call [hideLoading](${mainSitePath}/api.html#echartsInstance.hideLoading) to hide the animation.

```js
myChart.showLoading();
$.get('data.json').done(function (data) {
    myChart.hideLoading();
    myChart.setOption(...);
});
```

Here is the effect:

<md-example src="doc-example/tutorial-loading"></md-example>

## 동적 업데이트

ECharts는 데이터에 의해 구동되며, 데이터의 변화는 차트 표시의 변화를 이끌어냅니다. 따라서 동적 업데이트를 구현하는 것은 놀라울 정도로 간단합니다.

모든 데이터의 업데이트는 [setOption](${mainSitePath}/api.html#echartsInstance.setOption)으로 구현됩니다. 주기적으로 데이터를 가져오기만 하면 됩니다. ECharts는 두 그룹의 데이터 간의 차이를 찾아 적절한 방닝으로 애니메이션을 선택합니다.

다음 예제를 확인하세요.

<md-example src="doc-example/tutorial-dynamic-data"></md-example>
