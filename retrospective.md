### 26.01.30

라이브러리 비교할 때 A vs B vs C를 잘 정리한 문서를 찾으려고 하는데, 결국 좋은 문서를 찾아다니면서 시간 낭비하는 거 보다 각 라이브러리 공식 문서를 직접 들어가서 읽는 게 훨씬 더 효과적인 것 같다.

## 26.02.02

1. tanstack-query에서 하나의 서비스 로직이 무조건 useSuspenseQuery로만 존재하지 않는다. useQuery로도 존재할 수 있다. 언제 이득이 되냐면 UI에 영향을 받지 않는 로직에서 영향이 된다. 로직은 UI로 드러나지 않기 때문에 스피너가 필요하진 않지만, 만약 특정 로직이 서버 상태에 의존적이라면 어쨋든 서비스 로직이 한 번은 실행돼야 한다.

2. 함수명은 `handle` + `bahavior` + `ui descirption` 이 기본이지만, 이 구조가 겹치는 경우가 종종 존재. 예를들면, 모달을 띄우는 버튼, 모달 내에 존재하는 Positive Button은 겹치기 쉽다. 예를들면, `handleClickAddItemButton`으로 아이템을 등록하는 모달을 띄우고, 입력칸을 채운 다음  add item 버튼을 클릭할 때 이벤트 핸들러 역시도 동일하게 작성된다. 이때는 `handle` + `function` + `ui`로 작성한다. 즉, `handleOpenAddMachineModal`이 될 수 있다. 만약 하나의 핸들러가 여러 곳에서 사용되는 경우, `handle`을 생략한다. 아이템 추가 모달의 backdrop이나 cancel 버튼, add item 버튼을 누르면 모달을 닫는 로직이 동일하게 동작한다. `handleClickAddItem` 내에 `handleCloseAddItemModal`을 넣기에는 어색하니 그냥 `closeAddItemModal`정도로 타협을 보면 될 듯 하다. 


## 26.02.03

1.

어떤 로직이 특정 바운더리 내에서 동작한다는 것은 그만큼 자유도가 떨어진다는 의미같다. useSuspenseQuery가 그런듯? 

2.

dependent query가 존재하는 query는 dependent 하는 파라미터 타입을 optional 파라미터로 만드는건 필연적인듯. 왜냐하면 앞의 query가 끝나기 전까지는 당연하게도 파라미터가 undefined기 때문에.

3.

FE 변수명에 괜히 BE 변수명을 `억지로` 침투시키는 것은 좋지 않은 것 같다. 가령, 차량 모델을 추가할 때 Create, Update를 쓰기보다는 Add, Edit를 쓰는게 좋은 것 같다. 

약간 FE는 1순위로 행위를 변수명에 녹이고 2순위로 CRUD를 녹인다고 한다면 BE는 1순위로 CRUD를 변수명에 녹이고 2순위로 행위를 녹이는 방향성이 좋은 듯.