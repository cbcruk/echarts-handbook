# 워터폴 차트

Apache ECharts에는 워터폴 시리즈가 없지만, 누적 막대 차트를 사용하여 효과를 시뮤레이션할 수 있습니다.

데이터 배열의 값들이 이전 값에서의 증가 또는 감소를 나타낸다고 가정합시다.

```js
var data = [900, 345, 393, -108, -154, 135, 178, 286, -119, -361, -203];
```

즉, 첫 번째 데이터는 `900`이고 두 번째 데이터 `345`는 `900`에 `345`를 더한 것을 나타냅니다. 이 데이터를 단계별 워터폴 차트로 표시할 때, 세 개의 시리즈를 사용할 수 있습니다: 첫 번째는 비대화형 투명 시리즈로 현수 막대 효과를 구현하고, 두 번째 시리즈는 양수를 나타내며, 세 번째 시리즈는 음수를 나타냅니다.

```js live
var data = [900, 345, 393, -108, -154, 135, 178, 286, -119, -361, -203];
var help = [];
var positive = [];
var negative = [];
for (var i = 0, sum = 0; i < data.length; ++i) {
  if (data[i] >= 0) {
    positive.push(data[i]);
    negative.push('-');
  } else {
    positive.push('-');
    negative.push(-data[i]);
  }

  if (i === 0) {
    help.push(0);
  } else {
    sum += data[i - 1];
    if (data[i] < 0) {
      help.push(sum + data[i]);
    } else {
      help.push(sum);
    }
  }
}

option = {
  title: {
    text: '워터폴'
  },
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  xAxis: {
    type: 'category',
    splitLine: { show: false },
    data: (function() {
      var list = [];
      for (var i = 1; i <= 11; i++) {
        list.push('Oct/' + i);
      }
      return list;
    })()
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      type: 'bar',
      stack: 'all',
      itemStyle: {
        normal: {
          barBorderColor: 'rgba(0,0,0,0)',
          color: 'rgba(0,0,0,0)'
        },
        emphasis: {
          barBorderColor: 'rgba(0,0,0,0)',
          color: 'rgba(0,0,0,0)'
        }
      },
      data: help
    },
    {
      name: '양수',
      type: 'bar',
      stack: 'all',
      data: positive
    },
    {
      name: '음수',
      type: 'bar',
      stack: 'all',
      data: negative,
      itemStyle: {
        color: '#f33'
      }
    }
  ]
};
```
