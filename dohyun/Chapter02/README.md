# 리팩터링 원칙

## 리팩터링 정의

- 리팩터링[명사]: 소프트웨어의 겉보기 동작은 그대로 유지한 채, 코드를 이해하고 수정하기 쉽도록 내부 구조를 변경하는 기법
- 리팩터링[동사]: 소프트웨어의 겉보기 동작은 그대로 유지한 채, 여러 가지 리팩터링 기법을 적용해서 소프트웨어를 재구성한다.

> 리팩터링하는 동안에는 코드가 항상 정상 작동하기 때문에 전체 작업이 끝나지 않았더라도 언제든지 멈출 수 있다. 누군가 "리팩터링하다가 코드가 깨져서 며칠이나 고생했다."라고 한다면, 십중팔구 리팩터링한 것이 아니다.

<br />
<br />

## 리팩터링하는 이유

<br />

### 📌 리팩터링하면 소프트웨어 설계가 좋아진다.

리팩터링하지 않으면 소프트웨어의 내부 설계(아키텍처)가 썩기 쉽다. 아키텍처를 충분히 이해하지 못한 채 단기 목표만을 위해 코드를 수정하다 보면 기반 구조가 무너지기 쉽다. 그러면 코드만 봐서는 설계를 파악하기 어려워진다. 코드 구조가 무너지기 시작하면 악효과가 누적된다. 코드만으로 설계를 파악하기 어려워질수록 설계를 유지하기 어려워지고, 설계가 부패되는 속도는 더욱 빨라진다. 반면 규칙적인 리팩터링은 코드의 구조를 지탱해줄 것이다.

<br />

### 📌 리팩터링하면 소프트웨어를 이해하기 쉬워진다.

프로그래밍은 여러 면에서 마치 컴퓨터와 대화하는 것과 같다. 컴퓨터에게 시킬 일을 표현하는 코드를 작성하면, 컴퓨터는 정확히 시킨 대로 반응한다. 그런데 내 소스 코드를 컴퓨터만 사용하는 게 아니다. 예컨데 몇 달이 지나 누군가 내 코드를 수정하고자 읽게 될 수 있다. 다른 프로그래머가 내 코드를 제대로 이해했다면 한 시간에 끝낼 수정을 일주일이나 걸린다면 문제다. 리팩터링은 코드가 더 잘 읽히게 도와주고, 코드의 목적이 더 잘 드러나며 내 의도를 더 명확하게 전달하도록 개선할 수 있다.

<br />

### 📌 리팩터링하면 버그를 쉽게 찾을 수 있다.

코드를 이해하기 쉽다는 말은 버그를 찾기 쉽다는 말이기도 한다. 리팩터링하면 코드가 하는 일을 깊이 파악하게 되면서 새로 깨달은 것을 곧바로 코드에 반영하게 된다. 프로그램의 구조를 명확하게 다듬으면 그냥 "이럴 것이다"라고 가정하던 점들이 분명히 드러나는데, 버그를 지나치려야 지날칠 수 없을 정도까지 명확해진다.

<br />

### 📌 리팩터링하면 프로그래밍 속도를 높일 수 있다.

한 시스템을 오래 개발 중인 개발자들은 "초기에는 진척이 빨랐지만 현재는 새 기능을 하나 추가하는 데 훨씬 오래 걸린다"라는 말을 많이 한다. 새로운 기능을 추가할수록 기존 코드베이스에 잘 녹여낼 방법을 찾는 데 드는 시간이 늘어난다는 것이다. 게다가 기능을 추가하고 나면 버그가 발생하는 일이 잦고, 이를 해결하는 시간은 한층 더 걸린다. 이러한 부담이 기능 추가 속도를 계속 떨어뜨리면서, 차라리 처음부터 새로 개발하는 편이 낫겠다고 생각하는 지경에 이른다.

내부 설계가 잘 된 소프트웨어는 새로운 기능을 추가할 지점과 어떻게 고칠지를 쉽게 찾을 수 있다. 모듈화가 잘 되어 있으면 전체 코드베이스 중 작은 일부만 이해하면 된다. 코드가 명확하면 버그를 만들 가능성도 줄고, 버그를 만들더라도 디버깅하기가 훨씬 쉽다. 내부 품질이 뛰어난 코드베이스는 새 기능 구축을 돕는 견고한 토대가 된다.

<br />
<br />

## 언제 리팩터링해야 할까?

<br />

### 🔨 준비를 위한 리팩터링: 기능을 쉽게 추가하게 만들기

리팩터링하기 가장 좋은 시점은 코드베이스에 기능을 새로 추가하기 직전이다. 이 시점에 현재 코드를 살펴보면서, 구조를 살짝 바꾸면 다른 작업을 하기가 훨씬 쉬워질 만한 부분을 찾아서 리팩토링을 한다. 이처럼 준비를 위한 리팩터링으로 상황을 개선해놓으면 버그가 수정된 상태가 오래 지속될 가능성을 높이는 동시에, 같은 곳에서 다른 버그가 발생할 가능성을 줄일 수도 있다.

<br />

### 🔨 이해를 위한 리팩터링: 코드를 이해하기 쉽게 만들기

코드를 수정하려면 먼저 그 코드가 하는 일을 파악해야 한다. 그 코드를 작성한 사람은 자신일 수도 있고 다른 사람일 수도 있다. 코드가 깔끔하게 정리되어 있으면, 전에는 보이지 않던 설계가 눈에 들어오기 시작한다. 코드를 분석할 때 리팩터링을 해보면, 그렇지 않았더라면 도달하지 못했을 더 깊은 수준까지 이해하게 된다.

<br />

### 🔨 쓰레기 줍기 리팩터링

코드를 파악하던 중에 일을 비효율적으로 처리하는 모습을 발견할 때가 있다. 로직이 쓸게없이 복잡하거나, 매개변수화한 함수 하나면 될 일을 거의 똑같은 함수 여러 개로 작성해놨을 수 있다. 원래 하려던 작업과 관련 없는 일에 너무 많은 시간을 빼앗기긴 싫을 것이다. 그렇다고 쓰레기가 나뒹굴게 방치해서 나중에 일을 방해하도록 내버려두는 것도 좋지않다. 수정하려면 몇 시간이나 걸리고 당장은 더 급한 일이 있을 수 있다. 그렇더라도 조금이나마 개선해두는 것이 좋다.

<br />

### 🔨 계획된 리팩터링과 수시로 하는 리팩터링

보기 싫은 코드를 발견하면 리팩터링하자. 그런데 잘 작성된 코드 역시 수많은 리팩터링을 거쳐야한다. 무언가 수정하려 할 때는 먼저 수정하기 쉽게 정돈하고(단, 만만치 않을 수 있다) 그런 다음 쉽게 수정하자. 그동안 리팩터링에 소흘했다면, 따로 시간을 내서 새 기능을 추가하기 쉽도록 코드베이스를 개선할 필요가 있다. 이때 리팩터링에 투자한 일주일의 효과를 다음 몇 달 동안 누릴 수도 있다. 그러나 계획된 리팩터링을 하게 되는 일은 최소한으로 줄여야 한다. 리팩터링 작업 대부분은 드러나지 않게, 기회가 될 때마다 해야한다.

<br />

### 🔨 코드 리뷰에 리팩터링 활용하기

코드 리뷰는 개발팀 전체에 지식을 전파하는 데 좋다. 경험이 더 많은 개발자의 노하우를 더 적은 개발자에게 전수할 수 있다. 대규모 소프트웨어 시스템의 다양한 측면을 더 많은 사람이 이해하는 데도 도움된다. 깔끔한 코드를 작성하는 데에도 굉장히 중요하다. 내 눈에는 명확한 코드가 다른 팀원에게는 그렇지 않을 수 있다. 코드리뷰에 리팩터링을 접목하는 구체적인 방법은 리뷰의 성격에 따라 다르다. 흔히 쓰는 풀리퀘스트(코드 작성자 없이 검토하는 방식)에서는 그리 효과적이지 않다. 코드 작성자가 참석해야 맥락을 설명해줄 수 있고 작성자도 리뷰어의 변경 의도를 제대로 이해할 수 있으므로, 이왕이면 작성자가 참석하는 방식이 좋다. 작가가 경험한 가장 좋은 방법은 작성자와 나란히 앉아서 코드를 훑어가면서 리팩터링하는 것이다. 이렇게 하면 자연스럽게(프로그래밍 과정 안에 지속적인 코드 리뷰가 녹아 있는) `짝 프로그래밍`이 된다.

<br />
<br />

## 리팩터링 시 고려할 문제

<br />

### ⚠ 새 기능 개발 속도 저하

많은 사람이 리팩터링 때문에 새 기능을 개발하는 속도가 느려진다고 여기지만, 리팩터링의 궁극적인 목적은 개발 속도를 높이는 데 있다. 하지만 리팩터링으로 인해 진행이 느려진다고 생각하는 사람이 여전히 많다. 아마도 이 점이 실전에서 리팩터링을 제대로 적용하는 데 가장 큰 걸림돌인 것 같다.

> 리팩터링의 궁극적인 목적은 개발 속도를 높여서, 더 적은 노력으로 더 많은 가치를 창출하는 것이다.

<br />

### ⚠ 코드 소유권

리팩터링하다 보면 모듈의 내부뿐 아니라 시스템의 다른 부분과 연동하는 방식에도 영향을 주는 경우가 많다. 함수 이름을 바꾸고 싶고 그 함수를 호출하는 곳을 모두 찾을 수 있다면, 간단히 `함수 선언바꾸기`로 선언 자체와 호출하는 곳 모두를 한번에 바꿀 수 있다. 하지만 이렇게 간단하지 않을 때도 있다. 함수를 호출하는 코드의 소유자가 다른 팀이라서 나에게는 쓰기 권한이 없을 수 있다. 또는 바꾸려는 함수가 고객에게 API로 제공된 것이라면 누가 얼마나 쓰고 있는지를 고사하고, 실제로 쓰이기나 하는지조차 모를 수 있다. 이런 함수는 인터페이스를 누가 선언했는지에 관계없이 클라이언트가 사용하는 '공개된 인터페이스'에 속한다. 코드 소유권이 나뉘어 있으면 리팩터링에 방해가 된다. 클라이언트에 영향을 주지 않고서는 원하는 형태로 변경할 수 없기 때문이다. 그렇다고 리팩터링을 할 수 없는건 아니다. 여전히 훌륭하게 개선할 수 있지만 제약이 따를 뿐이다.

<br />

### ⚠ 테스팅

리팩터링의 두드러진 특성은 프로그램의 겉보기 동작은 똑같이 유지된다는 것이다. 절차를 지켜 제대로 리팩터링하면 동작이 깨지지 않아야 한다. 하지만 실수를 저지른다면? 실수하더라도 재빨리 해결하면 문제가 되지 않는다. 리팩터링은 단계별 변경 폭이 작아서 도중에 발생한 오류의 원인이 될만한 코드 범위가 넓지 않다. 원인을 못 찾더라도 버전 관리 시스템을 이용하여 가장 최근에 정상 작동하던 상태로 되돌리면 된다. 여기서 핵심은 오류를 재빨리 잡는 데 있다. 실제로 이렇게 하려면 코드의 다양한 측면을 검사하는 `테스트 스위트`가 필요하다. 그리고 이를 빠르게 실행할 수 있어야 수시로 테스트하는 데 부담이 없다. 달리 말하면 리팩터링하기 위해서는 (대부분의 경우에) 자가 테스트 코드 를 마련해야 한다는 뜻이다.

<br />

