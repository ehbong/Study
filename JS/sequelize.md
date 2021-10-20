# Sequelize

* [시퀄라이즈 공식문서](https://sequelize.org/master/)
* [공식문서 번역 글](https://loy124.tistory.com/294)
* [관계 설정](https://velog.io/@josworks27/Sequelize-Association)
* [관계 정의하기](https://loy124.tistory.com/294)
* [DB모델 자동 생성sequelize-auto](https://github.com/sequelize/sequelize-auto)
* [테이블 변경 사항 적용하기 마이그레이션](https://jeonghwan-kim.github.io/sequelize-migration/)
* [트랜젝션 사용방법](https://sequelize.org/master/manual/transactions.html)

#### Raw query 사용법
* [공식문서 Raw Queries](https://sequelize.org/master/manual/raw-queries.html)
```javascript
const { QueryTypes } = require('sequelize');
const users = await sequelize.query("SELECT * FROM `users`", { type: QueryTypes.SELECT });
```

#### Join
```javascript
<Model>.findAll({
     include: [
        {
          model: <조인할 Model>,
          attributes: [<필요한컬럼 리스트>]
        }
     ],
     where: {<조건식>},
});
```
