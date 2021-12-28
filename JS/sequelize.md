# Sequelize

* [시퀄라이즈 공식문서](https://sequelize.org/master/)
* [공식문서 번역 글](https://loy124.tistory.com/294)
* [관계 설정](https://velog.io/@josworks27/Sequelize-Association)
* [관계 정의하기](https://loy124.tistory.com/294)
* [DB모델 자동 생성sequelize-auto](https://github.com/sequelize/sequelize-auto)
* [테이블 변경 사항 적용하기 마이그레이션](https://jeonghwan-kim.github.io/sequelize-migration/)
* [트랜젝션 사용방법](https://sequelize.org/master/manual/transactions.html)
* [튜토리얼](https://soogoonsoogoonpythonists.github.io/sqlalchemy-for-pythonist/tutorial/6.%20ORM%20%EB%B0%A9%EC%8B%9D%EC%9C%BC%EB%A1%9C%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%A1%B0%EC%9E%91%ED%95%98%EA%B8%B0.html#orm%E1%84%8B%E1%85%B3%E1%84%85%E1%85%A9-%E1%84%92%E1%85%A2%E1%86%BC-%E1%84%89%E1%85%A1%E1%86%B8%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5)

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
#### Operators
```javascript
const { Op } = require("sequelize");
Post.findAll({
  where: {
    [Op.and]: [{ a: 5 }, { b: 6 }],            // (a = 5) AND (b = 6)
    [Op.or]: [{ a: 5 }, { b: 6 }],             // (a = 5) OR (b = 6)
    someAttribute: {
      // Basics
      [Op.eq]: 3,                              // = 3
      [Op.ne]: 20,                             // != 20
      [Op.is]: null,                           // IS NULL
      [Op.not]: true,                          // IS NOT TRUE
      [Op.or]: [5, 6],                         // (someAttribute = 5) OR (someAttribute = 6)

      // Using dialect specific column identifiers (PG in the following example):
      [Op.col]: 'user.organization_id',        // = "user"."organization_id"

      // Number comparisons
      [Op.gt]: 6,                              // > 6
      [Op.gte]: 6,                             // >= 6
      [Op.lt]: 10,                             // < 10
      [Op.lte]: 10,                            // <= 10
      [Op.between]: [6, 10],                   // BETWEEN 6 AND 10
      [Op.notBetween]: [11, 15],               // NOT BETWEEN 11 AND 15

      // Other operators

      [Op.all]: sequelize.literal('SELECT 1'), // > ALL (SELECT 1)

      [Op.in]: [1, 2],                         // IN [1, 2]
      [Op.notIn]: [1, 2],                      // NOT IN [1, 2]

      [Op.like]: '%hat',                       // LIKE '%hat'
      [Op.notLike]: '%hat',                    // NOT LIKE '%hat'
      [Op.startsWith]: 'hat',                  // LIKE 'hat%'
      [Op.endsWith]: 'hat',                    // LIKE '%hat'
      [Op.substring]: 'hat',                   // LIKE '%hat%'
      [Op.iLike]: '%hat',                      // ILIKE '%hat' (case insensitive) (PG only)
      [Op.notILike]: '%hat',                   // NOT ILIKE '%hat'  (PG only)
      [Op.regexp]: '^[h|a|t]',                 // REGEXP/~ '^[h|a|t]' (MySQL/PG only)
      [Op.notRegexp]: '^[h|a|t]',              // NOT REGEXP/!~ '^[h|a|t]' (MySQL/PG only)
      [Op.iRegexp]: '^[h|a|t]',                // ~* '^[h|a|t]' (PG only)
      [Op.notIRegexp]: '^[h|a|t]',             // !~* '^[h|a|t]' (PG only)

      [Op.any]: [2, 3],                        // ANY ARRAY[2, 3]::INTEGER (PG only)

      // In Postgres, Op.like/Op.iLike/Op.notLike can be combined to Op.any:
      [Op.like]: { [Op.any]: ['cat', 'hat'] }  // LIKE ANY ARRAY['cat', 'hat']

      // There are more postgres-only range operators, see below
    }
  }
});
```
