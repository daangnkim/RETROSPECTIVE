## UI/UX

모달에서 CREATE, UPDATE, DELETE 후에 모달을 닫는 상황을 생각해보자.
그리고 tanstack query를 이용하고 있다.

모달을 열었을 때 CREATE, UPDATE, DELETE 작업을 진행하고 모달을 닫는게 좋을까?
아니면 tanstack query 내의 onSuccess가 성공했을 때 닫는게 좋을까?
아니면 tanstack query 내의 onSettled가 성공했을 때 닫는게 좋을까?
