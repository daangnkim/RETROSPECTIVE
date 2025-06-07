개인적으로 컴포넌트를 분리하는 기준은 다음과 같다.

1. 재사용되진 않지만 하나의 컴포넌트로 두기에는 너무 복잡할 때 적절한 책임에 따라 나눈다.
2. 재사용되며 변경 빈도가 적을 때 나눈다. 그리고 이 과정에서 여러 패턴을 고민한다.

다만 DRY 원칙이 WET 원칙보다 비용이 더 높을 수 있다는 점은 인지한다.

## 다양한 패턴이란

1. 성능에 의한 분리

   부모 컴포넌트가 Header 컴포넌트로 인해 리렌더링 되지 않아도 된다. Layout 내에 Header, Outlet 컴포넌트가 존재할 때, Outlet이 리렌더링될 일이 없다. useNavigate는 리렌더링 이슈가 있었는데, Header 컴포넌트 내부에 포함시켜서 리렌더링을 면했다.

2. render prop

   react-hook-form의 Controller 컴포넌트처럼 상태를 자식 컴포넌트에서 부모 컴포넌트로 끌어올릴 수 있다. 내부의 구체적인 구현사항은 모르나 필요한 명세만 노출되므로 로직이 추상화된다.

3. compound

   Header 컴포넌트를 구현할 때, 왼쪽과 오른쪽 끝에는 1개 이상의 버튼이 존재할 수 있고, 가운데는 텍스트가 존재할 수 있다. Header.Left, Header.Right, Header.Center를 이용해서 semantic한 태그구조 주입이 가능하지만 약속한 형태로 컴포넌트를 넘겨야한다는 단점이 존재한다.

4. HOC

   한 곳에 구현한 로직을 여러 컴포넌트에서 재사용 가능하다. 더불어서 관심사의 분리도 가능하다. 하지만 prop의 이름이 겹칠수도 있다는 단점이 존재한다.

[Patterns.dev.kr](https://patterns-dev-kr.github.io/design-patterns/render-props-pattern/)
