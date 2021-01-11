


    테스트 테이블

      +-------+---------+------+-----+---------+----------------+
      | Field | Type    | Null | Key | Default | Extra          |
      +-------+---------+------+-----+---------+----------------+
      | id    | int(11) | NO   | PRI | NULL    | auto_increment |
      | code  | int(10) | YES  |     | NULL    |                |
      +-------+---------+------+-----+---------+----------------+

      +----------+
      | count(*) |
      +----------+
      |  3196102 |
      +----------+





    group by + having

      select code,count(code) from lab.having_test group by(code) having code=2;

      1 row in set (0.98 sec)

      1 row in set (0.98 sec)

      1 row in set (0.98 sec)


    group by + where 절 

      select code,count(code) from lab.having_test where code = 2 group by(code);

      1 row in set (0.44 sec)

      1 row in set (0.44 sec)

      1 row in set (0.44 sec)



    결론
      group by + where : 0.44 sec
      group by + having : 0.98 sec
      증감율 : 약 122 %

      group by 구문에 조건을 걸 경우 where 절을 사용하는 게 더 빠르다
