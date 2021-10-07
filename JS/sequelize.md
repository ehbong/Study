# Sequelize

* [시퀄라이즈 공식문서](https://sequelize.org/master/)

* [관계 설정](https://velog.io/@josworks27/Sequelize-Association)
* [DB모델 자동 생성sequelize-auto](https://github.com/sequelize/sequelize-auto)
* [테이블 변경 사항 적용하기 마이그레이션](https://jeonghwan-kim.github.io/sequelize-migration/)

#### Raw query 사용법
* [공식문서 Raw Queries](https://sequelize.org/master/manual/raw-queries.html)
```javascript
const { QueryTypes } = require('sequelize');
const users = await sequelize.query("SELECT * FROM `users`", { type: QueryTypes.SELECT });
```
