1. 모든 파일들을 ts로 바꾸고, 발생하는 타입 에러에 대해서는 noImplicitAny와 함께 any 타입을 적용한다.
2. dependency cruiser를 통해 모듈들에 대한 의존성을 시각화한뒤 가장 최하단 모듈들부터 Bottom Up으로 마이그레이션한다.
3. jsdoc을 적극 활용한다.