# 데이터 전환

Apache ECharts<sup>TM</sup>는 데이터를 추가, 업데이트, 제거할 때 위치, 크기, 모양에 전환 애니메이션을 적용합니다. 이를 통해 차트가 더 부드러워지고 데이터 간의 관계를 더 잘 보여줍니다. 개발자는 대부분 애니메이션 사용법에 대해 걱정할 필요가 없으며, 단순히 `setOption`을 사용하여 데이터를 업데이트하면 ECharts가 마지막 데이터와의 차이점을 찾아 자동으로 가장 적절한 전환 애니메이션을 적용합니다.

예를 들어, 다음 예시는 파이 차트 데이터의 시간별 업데이트에 대한 전환을 보여줍니다.

```js live {layout: 'lr'}
function makeRandomData() {
  return [
    {
      value: Math.random(),
      name: 'A'
    },
    {
      value: Math.random(),
      name: 'B'
    },
    {
      value: Math.random(),
      name: 'C'
    }
  ];
}
option = {
  series: [
    {
      type: 'pie',
      radius: [0, '50%'],
      data: makeRandomData()
    }
  ]
};

setInterval(() => {
  myChart.setOption({
    series: {
      data: makeRandomData()
    }
  });
}, 2000);
```

## 전환 구성

데이터 추가와 업데이트는 종종 다른 애니메이션이 필요하며(예를 들어 데이터 업데이트 애니메이션이 더 짧기를 기대), ECharts는 두 가지 애니메이션 구성을 구분합니다.

- 데이터 추가의 경우, 진입 애니메이션을 적용하며 `animationDuration`, `animationEasing`, `animationDelay`를 사용하여 애니메이션의 지속시간, 이징, 지연시간을 각각 구성합니다.
- 데이터 업데이트의 경우, `animationDurationUpdate`, `animationEasingUpdate`, `animationDelayUpdate`로 애니메이션의 지속시간, 이징, 지연시간을 각각 구성하는 업데이트 애니메이션을 적용합니다.

보시다시피, 업데이트 애니메이션 구성은 진입 애니메이션 구성에 `Update` 접미사가 붙은 것입니다.

> ECharts에서 setOption을 사용할 때마다 데이터는 마지막으로 업데이트된 데이터와 차이를 비교하고, 차이 결과에 따라 데이터에 대해 추가, 업데이트, 제거의 세 가지 상태가 수행됩니다. 이 차이 비교는 데이터의 `name`을 기반으로 하며, 예를 들어 마지막 업데이트가 `'A'`, `'B'`, `'C'`라는 세 개의 `name`을 가지고 있었고, 새 업데이트에서 `'B'`, `'C'`, `'D'`가 되었다면, 데이터 `'B'`, `'C'`는 업데이트되고, 데이터 `'A'`는 제거되며, 데이터 `'D'`는 추가됩니다. 처음으로 `setOption`을 사용하는 경우, 이전 데이터가 없기 때문에 모든 데이터가 추가됩니다. 세 가지 상태에 따라 ECharts는 각각 진입 애니메이션, 업데이트 애니메이션, 퇴장 애니메이션을 적용합니다.

이러한 모든 구성은 모든 시리즈와 컴포넌트에 대해 `option`의 최상위 레벨에서 설정하거나 각 시리즈에 대해 별도로 설정할 수 있습니다.

애니메이션을 끄려면 간단히 `option.animation`을 `false`로 설정하면 됩니다.

### 애니메이션 지속시간

`animationDuration`과 `animationDurationUpdate`는 애니메이션의 지속시간을 `ms` 단위로 설정하는 데 사용됩니다. 더 긴 애니메이션 지속시간을 설정하면 사용자가 전환 애니메이션 효과를 더 명확하게 볼 수 있지만, 너무 오래 걸리면 사용자가 애니메이션이 끝나기를 기다리는 동안 인내심을 잃을 수 있으므로 주의해야 합니다.

`0`으로 설정하면 애니메이션이 꺼지며, 진입 애니메이션이나 업데이트 애니메이션만 끄려는 경우 해당 구성을 개별적으로 `0`으로 설정하여 이를 달성할 수 있습니다.

### 애니메이션 이징

`animationEasing`과 `animationEasingUpdate` 구성 항목은 애니메이션의 이징 함수를 설정하는 데 사용되며, 이는 애니메이션 시간을 입력받아 애니메이션 진행률을 출력하는 함수입니다.

```ts
(t: number) => number;
```

`'cubicIn'` 및 `'cubicOut'`과 같은 일반적인 애니메이션 이징 함수는 ECharts에 내장되어 있어 직접 사용할 수 있습니다.

내장된 이징 함수들:

<md-example src="line-easing" width="100%" height="400" />

### 애니메이션 지연

`animationDelay`와 `animationDelayUpdate`는 애니메이션 지연 시작 시간을 설정하는 데 사용되며, 일반적으로 콜백 함수를 사용하여 다른 데이터에 대해 다른 지연을 설정하여 엇갈린 애니메이션 효과를 달성합니다:

```ts live { layout: 'lr' }
var xAxisData = [];
var data1 = [];
var data2 = [];
for (var i = 0; i < 100; i++) {
  xAxisData.push('A' + i);
  data1.push((Math.sin(i / 5) * (i / 5 - 10) + i / 6) * 5);
  data2.push((Math.cos(i / 5) * (i / 5 - 10) + i / 6) * 5);
}
option = {
  legend: {
    data: ['bar', 'bar2']
  },
  xAxis: {
    data: xAxisData,
    splitLine: {
      show: false
    }
  },
  yAxis: {},
  series: [
    {
      name: 'bar',
      type: 'bar',
      data: data1,
      emphasis: {
        focus: 'series'
      },
      animationDelay: function(idx) {
        return idx * 10;
      }
    },
    {
      name: 'bar2',
      type: 'bar',
      data: data2,
      emphasis: {
        focus: 'series'
      },
      animationDelay: function(idx) {
        return idx * 10 + 100;
      }
    }
  ],
  animationEasing: 'elasticOut',
  animationDelayUpdate: function(idx) {
    return idx * 5;
  }
};
```

## 애니메이션의 성능 최적화

데이터 양이 특히 많을 때 애니메이션 실행은 성능 문제가 있을 수 있으므로, `animation: false`를 설정하여 애니메이션을 끌 수 있습니다.

데이터 양이 동적으로 변하는 차트의 경우, `animationThreshold` 구성을 사용하는 것을 권장합니다. 이를 통해 캔버스의 그래프 수가 이 임계값을 초과할 때 ECharts가 자동으로 애니메이션을 끄어 그리기 성능을 향상시킬 수 있습니다. 이는 종종 경험적 값이며, ECharts는 일반적으로 실시간으로 수천 개의 그래프를 렌더링할 수 있습니다(기본값도 2000으로 설정됨). 하지만 차트가 복잡하거나 사용자 환경이 열악하고 페이지에서 동시에 실행되는 다른 복잡한 코드가 많은 경우, 전체 애플리케이션의 원활함을 보장하기 위해 이 값을 적절히 낮추는 것이 좋을 수 있습니다.

## 애니메이션 종료 감지

때로는 현재 렌더링 결과를 얻고 싶을 때가 있습니다. 애니메이션을 사용하지 않는다면, ECharts는 `setOption` 후 직접 렌더링을 수행하고 `getDataURL` 메서드를 사용하여 동기적으로 렌더링 결과를 얻을 수 있습니다.

```ts
const chart = echarts.init(dom);
chart.setOption({
  animation: false
  //...
});
// 직접 동기적으로 실행 가능
const dataUrl = chart.getDataURL();
```

하지만 차트에 애니메이션이 있는 경우, `getDataURL`을 즉시 실행하면 최종 결과가 아닌 애니메이션 시작 시점의 그림을 얻게 됩니다. 따라서 애니메이션이 완료된 시점을 알고 난 후 `getDataURL`을 실행하여 결과를 얻어야 합니다.

애니메이션의 지속시간을 확실히 안다면, 더 간단하고 직접적인 방법은 애니메이션 지속시간에 따라 `setTimeout`으로 실행을 지연시키는 것입니다:

```ts
chart.setOption({
  animationDuration: 1000
  //...
});
setTimeout(() => {
  const dataUrl = chart.getDataURL();
}, 1000);
```

또는 ECharts에서 제공하는 `rendered` 이벤트를 사용하여 ECharts가 애니메이션을 완료하고 렌더링을 중단했음을 확인할 수 있습니다.

```ts
chart.setOption({
  animationDuration: 1000
  //...
});

function onRendered() {
  const dataUrl = chart.getDataURL();
  // ...
  // 이후 상호작용이 있고 상호작용으로 다시 그려지는 경우에도 이 이벤트가 트리거되므로, 사용을 완료한 후에는 제거해야 합니다
  chart.off('rendered', onRendered);
}
chart.on('rendered', onRendered);
```
