# Sequelize

* [시퀄라이즈 공식문서](https://sequelize.org/master/)

* [관계 설정](https://velog.io/@josworks27/Sequelize-Association)

#### Raw query 사용법
* [공식문서 Raw Queries](https://sequelize.org/master/manual/raw-queries.html)
```javascript
const { QueryTypes } = require('sequelize');
const users = await sequelize.query("SELECT * FROM `users`", { type: QueryTypes.SELECT });
```
