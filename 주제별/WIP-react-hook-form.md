단점부터 말하면 러닝커브가 어느정도 있다. 이 러닝커브는 react-hook-form 뿐만이 아니라 zod, yup과 같은 validation 라이브러리에 대한 러닝커브를 포함한다.

장점을 말하면 다음과 같다.

1. ui에서 form 필드와 관련한 validaiton 코드가 사라진다.
   ```tsx
   {
     errors.email.length < schema.email.maxLength && <ErrorMessage />;
   }
   ```
2. value와 이벤트 핸들러를 일일히 할당하지 않아도 된다.
3. 에러가 있는 필드에 대한 auto focus도 지원된다.
