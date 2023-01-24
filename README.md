# DoneDone-Experience

> 던던은 모든 영역에서 최고의 경험을 제공하고자 합니다.

던던 리드인 성빈의 이전 프로젝트인 [덕키](https://github.com/duckie-team)에서 이루지 못한 목표와 얻은 교훈을 바탕으로 던던에서는 우리 모두에게 최상의 경험을 제공하고자 몇몇 가이드라인을 제공합니다.

## User

- 다양한 font-scale 을 존중합니다.
- 다양한 device-scale 을 존중합니다.
- 최선의 접근성을 제공합니다.
- 최선의 ux-writing 을 제공합니다.

## Developer

- 컴포넌트 사이즈 하드코딩을 지양합니다.
  - 다양한 font-scale 대응을 위해 패딩을 활용하여 사이즈를 측정합니다.
- device-scale 별로 layout 을 제작합니다. (MVP 다음 출시부터 제공)
  - 다양한 device-scale 을 존중해야 합니다. 
- 최소 터치 영역을 보장합니다.
  - 최선의 접근성을 위해 최소한의 터치 영역을 보장해야 합니다. 부족한 터치 영역은 패딩으로 확보할 수 있습니다.
  - 최소 터치 영역은 24dp 로 지정합니다.
- ux-writing 린트에 항상 warning 이 없게 유지하며 ux-writing in-app overlay 도 수시로 확인합니다.
  - DoneDone 의 경우 UI 에서 Text 가 차지하는 비중이 절대적으로 높습니다. 유저가 처음부터 끝까지 마주치는 영역이 Text 인 만큼, 1순위로 최상의 경험을 제공해야 합니다.
- 조기 최적화를 피합니다.
  - 수백만 명의 요청을 걱정하기 전에 100명의 사용자가 우리의 제품을 좋아하고 계속 사용하고 싶어 하는지를 먼저 확인해야 합니다. 사용자 피드백을 검증하는 작업이 우선입니다.
  - 대부분의 조기 최적화를 불필요하며 눈에 띄는 성능 문제가 관측됐을 때 진행해도 늦지 않습니다.
  - 적어도 제품 초기 단계에서는 최적화에 투자할 시간으로 기능 개발이나 유저 피드백 반영을 우선시해야 합니다. 제품 초기 단계에서는 우리가 작성한 코드가 삭제될 가능성이 높습니다.
  - Reference: [#1](https://stackify.com/premature-optimization-evil/) [#2](https://softwareengineering.stackexchange.com/questions/80084/is-premature-optimization-really-the-root-of-all-evil)
- 오버 엔지니어링을 피합니다.
  - 불필요한 추가 개발은 코드베이스의 복잡도를 증가시키고 코드 유지보수에 추가 비용을 초래합니다. 
  - 만약 지루함에서 오는 오버 엔지니어링(흥미로운 도전의 결과)이라면 안드로이드 개발팀 모두에게 새로운 경험인 [린트 개발](https://cosmos.donedone.me)에 참여하여 해소할 수 있습니다.
  - 내가 하려는 개발이 [DEEP](https://deep.donedone.me/) 에서 논의가 완료된 부분인지 확인해야 합니다.
  - Reference: [#1](https://en.wikipedia.org/wiki/Overengineering) [#2](https://www.mindtheproduct.com/overengineering-can-kill-your-product/)
- 코드베이스의 90% 이상을 파악하고 있어야 합니다. (세부 구현 방법까지는 불필요, 단순히 파악에만 의의를 둠)
  - 한 사람만 일방적으로 피드백하는 상황을 예방할 수 있습니다.
  - 코드 재사용으로 중복 코드를 예방할 수 있습니다.
  - 특정 상황에 사용하도록 설계된 코드를 적합하게 사용할 수 있습니다.
- 서로의 성장을 응원합니다.
  - 한 사람만 일방적으로 피드백하는 상황을 예방해야 합니다. 우리 모두가 피드백을 원합니다.
  - 고민이 오래갈 문제는 모두에게 공유합니다. 함께 고민하면 다 같이 성장하고 더 빠른 해결을 기대할 수 있습니다.
