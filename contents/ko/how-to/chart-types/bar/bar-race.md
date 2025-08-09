# 동적 정렬 막대 차트

## 관련 옵션

바 레이스는 시간에 따른 데이터 순위 변화를 보여주는 차트로, ECharts 5부터 기본적으로 지원됩니다.

> 바 레이스 차트는 일반적으로 가로 막대를 사용합니다. 세로 막대를 사용하려면 이 튜토리얼의 X축과 Y축을 반대로 설정하면 됩니다.

1. 막대 시리즈의 `realtimeSort`를 `true`로 설정하여 바 레이스를 활성화합니다
2. `yAxis.inverse`를 `true`로 설정하여 긴 막대가 위쪽에 표시되도록 합니다
3. `yAxis.animationDuration`은 첫 번째 막대 재정렬 애니메이션을 위해 `300`으로 설정하는 것이 권장됩니다
4. `yAxis.animationDurationUpdate`는 이후 막대 재정렬 애니메이션을 위해 `300`으로 설정하는 것이 권장됩니다
5. `yAxis.max`를 _n - 1_로 설정합니다. 여기서 _n_은 표시할 막대의 개수입니다. 그렇지 않으면 모든 막대가 표시됩니다
6. `xAxis.max`는 데이터의 최댓값이 X 최댓값으로 사용되도록 `'dataMax'`로 설정하는 것이 권장됩니다
7. 실시간 라벨 변경이 필요한 경우 `series.label.valueAnimation`을 `true`로 설정합니다
8. `animationDuration`을 `0`으로 설정하여 첫 번째 애니메이션이 0부터 시작하지 않도록 합니다. 다른 방식을 원한다면 `animationDurationUpdate`와 같은 값으로 설정하세요
9. `animationDurationUpdate`는 애니메이션 업데이트 지속 시간을 위해 `3000`으로 설정하는 것이 권장되며, 이는 `setOption` 호출 빈도와 같아야 합니다
10. `animationDurationUpdate` 빈도로 `setInterval`을 사용하여 `setOption`을 호출하여 다음 시간의 데이터로 업데이트합니다

## 데모

완전한 데모:

```js live
var data = [];
for (let i = 0; i < 5; ++i) {
  data.push(Math.round(Math.random() * 200));
}

option = {
  xAxis: {
    max: 'dataMax'
  },
  yAxis: {
    type: 'category',
    data: ['A', 'B', 'C', 'D', 'E'],
    inverse: true,
    animationDuration: 300,
    animationDurationUpdate: 300,
    max: 2 // only the largest 3 bars will be displayed
  },
  series: [
    {
      realtimeSort: true,
      name: 'X',
      type: 'bar',
      data: data,
      label: {
        show: true,
        position: 'right',
        valueAnimation: true
      }
    }
  ],
  legend: {
    show: true
  },
  animationDuration: 0,
  animationDurationUpdate: 3000,
  animationEasing: 'linear',
  animationEasingUpdate: 'linear'
};

function run() {
  var data = option.series[0].data;
  for (var i = 0; i < data.length; ++i) {
    if (Math.random() > 0.9) {
      data[i] += Math.round(Math.random() * 2000);
    } else {
      data[i] += Math.round(Math.random() * 200);
    }
  }
  myChart.setOption(option);
}

setTimeout(function() {
  run();
}, 0);
setInterval(function() {
  run();
}, 3000);
```
