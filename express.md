next(error)로 처리하면 이 뒤에 있는 일반 미들웨어는 전부 건너뛰고 이 에러를 바로 에러처리 미들웨어로 전달함

res 객체를 파라미터로 쓰는 함수를 만들지 말자

app.use() 이런 구조면 미들웨어

app.use(HandlerFn) - 전역 미들웨어
app.use(PATH, HandlerFn) - 특정 경로에 적용되는 미들웨어
app.get(PATH, HandlerFn) - 라우트 핸들러 (미들웨어의 일종)




