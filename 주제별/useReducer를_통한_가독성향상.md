# 효율적인 지도 필터링을 위한 FilterDrawer 리팩토링

`useState`의 대안인 `useReducer`는 복잡한 상태 관리를 좀 더 구조화하고 예측 가능하게 만든다. 그리고 liket에서 useState를 useReducer로 변경하여 가독성을 향상시켰다.

## 개요

liket에서는 지도에 컨텐츠들을 보여주고 컨텐츠들을 필터링할 수 있는 기능이 존재한다.

컨텐츠들은 STYLES, GENRE, AGE 정보를 가진다. 지도에서 이 정보들을 기반으로 필터링이 가능하다. 필터링을 위한 각 정보의 타입은 다음과 같다.

```typescript
interface MapFilter {
  styles: StyleEntity[];
  genre: GenreEntity | null;
  age: AgeEntity | null;
}
```

타입에서 알 수 있듯이, 셋 다 nullable하며, styles과 관련한 필터링은 여러 개가 적용이 가능하다.

그리고 이러한 필터링은 `<FilterDrawer/>` 컴포넌트를 통해서 적용한다.

## 문제

`<FilterDrawer/>`내에서 필터링 적용과 관련된 버튼들과 이벤트 핸들러의 설명은 다음과 같다

1. `<FilterDrawerCloseButton/>`

   닫기 버튼을 누르면 `<FilterDrawer/>`가 닫히고 이전 필터를 적용한다.

   ```jsx
   <Header>
     <HeaderLeft
       option={{
         close: {
           onClick: () => {
             onChangeDraftMapFilter({ ...appliedMapFilter });
             router.replace("/map");
           },
         },
       }}
     />
     <HeaderMiddle text="필터" />
   </Header>
   ```

2. `<StyleSelectButton/>`

   ```jsx

   ```

3. `<GenreSelectButton/>`
4. `<AgeSelectButton/>`
5. `<InitializationButton/>`
6. `<ApplyFilterButton/>`
