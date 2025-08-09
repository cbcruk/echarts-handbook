# 기본 막대 차트

막대 차트는 이산 데이터 간의 비교를 나타내는 차트입니다. 막대의 길이는 범주형 데이터와 비례 관계에 있습니다.

<iframe max-width="830" width="100%" height="400"
src="https://gallery.echartsjs.com/view-lite.html?cid=xS18jqmX4f">
</iframe>

시리즈의 레이블이 길거나 한 차트에 10개 이상의 범주가 있을 때, 수평 컬럼 차트는 모든 레이블을 표시할 수 없거나 레이블을 기울여서만 표시할 수 있습니다. 이는 적용성에 영향을 줍니다. 따라서 더 나은 표시 효과를 얻기 위해 수직 막대 차트를 사용합니다.

<iframe max-width="830" width="100%" height="400"
src="https://gallery.echartsjs.com/view-lite.html?cid=xByXtUE7Vz">
</iframe>

## 막대 차트 사용 제안

1. 너무 많은 색상 사용을 피하세요. 하나의 막대 차트는 일반적으로 하나의 메트릭 세트를 나타내므로 같은 색상이나 최소한 같은 색상의 다른 음영을 사용하는 것을 제안합니다. 의미 있는 데이터 포인트를 강조하기 위해 대비되는 색상을 사용할 수 있습니다.

<iframe max-width="830" width="100%" height="400"
src="https://gallery.echartsjs.com/view-lite.html?cid=xByYRlN7Ef">
</iframe>

2. 막대 사이의 간격은 적절해야 합니다. 너무 가까우면 사용자의 주의가 막대 사이의 간격에 집중될 수 있습니다. 합리적인 너비는 막대 사이의 간격의 두 배 이상이어야 합니다.

3. Y축의 데이터는 값을 적절히 반영하기 위해 0부터 시작해야 합니다. Y축이 불완전하면 사용자가 잘못된 판단을 하도록 오해를 일으킬 수 있습니다. 예를 들어, 왼쪽 차트는 2017년 수입이 2014년보다 4배 높다는 것을 보여줍니다. 하지만 오른쪽 차트는 2017년 수입이 2014년과 비교하여 25%만 증가했다는 진실을 보여줍니다.

<img max-width="830" width="100%" height="100%"
src="images/design/bar/bar03.jpg">
</img>

4. 여러 데이터를 정렬할 때, 날짜와 같은 특정 값과 관련이 없다면 특정 논리를 따르고 사용자가 직관적인 방식으로 데이터를 확인하도록 안내하는 것이 좋습니다. 간단히 말해, 논리적 정렬은 사용자가 어느 정도 데이터를 더 잘 읽도록 안내할 수 있습니다.

<iframe max-width="830" width="100%" height="400"
src="https://gallery.echartsjs.com/view-lite.html?cid=xHJhWhGm4M">
</iframe>

데이터 전송이 정확하지 않기 때문에 3D 막대 차트를 사용하는 것을 권장하지 않습니다. 사용자는 심지어 막대의 상단이 어디인지 추측해야 합니다.

<img max-width="830" width="100%" height="100%"
src="images/design/bar/bar04.jpg">
</img>