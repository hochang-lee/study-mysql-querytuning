
    테스트 테이블

      +-------+---------+------+-----+---------+----------------+
      | Field | Type    | Null | Key | Default | Extra          |
      +-------+---------+------+-----+---------+----------------+
      | id    | int(11) | NO   | PRI | NULL    | auto_increment |
      | val   | int(10) | YES  | MUL | NULL    |                |
      | val2  | int(10) | YES  | MUL | NULL    |                |
      | val3  | int(10) | YES  | MUL | NULL    |                |
      +-------+---------+------+-----+---------+----------------+


      +----------+
      | count(*) |
      +----------+
      |  1200012 |
      +----------+






    인덱스 컬럼 + 인덱스 컬럼 + 인덱스 컬럼

      | val   | int(10) | YES  | MUL | NULL    |                |
      | val2  | int(10) | YES  | MUL | NULL    |                |
      | val3  | int(10) | YES  | MUL | NULL    |                |

      select * from lab.index_equal_test where val=700000 and val2=700000 and val3=700000;

      100001 rows in set (0.10 sec)

      100001 rows in set (0.11 sec)

      100001 rows in set (0.11 sec)

    인덱스 컬럼 + 인덱스 컬럼 + 컬럼

      | val   | int(10) | YES  | MUL | NULL    |                |
      | val2  | int(10) | YES  | MUL | NULL    |                |
      | val3  | int(10) | YES  |     | NULL    |                |

      select * from lab.index_equal_test where val=700000 and val2=700000 and val3=700000;

      100001 rows in set (0.26 sec)

      100001 rows in set (0.27 sec)

      100001 rows in set (0.26 sec)


    인덱스 컬럼 + 컬럼 + 컬럼

      | val   | int(10) | YES  | MUL | NULL    |                |
      | val2  | int(10) | YES  |     | NULL    |                |
      | val3  | int(10) | YES  |     | NULL    |                |

      select * from lab.index_equal_test where val=700000 and val2=700000 and val3=700000;

      100001 rows in set (0.22 sec)

      100001 rows in set (0.22 sec)

      100001 rows in set (0.21 sec)

    컬럼 + 컬럼 + 컬럼

      select * from lab.index_equal_test where val=700000 and val2=700000 and val3=700000;

      100001 rows in set (0.24 sec)

      100001 rows in set (0.25 sec)

      100001 rows in set (0.25 sec)


    결론
      1)
      초기 테스트 때 데이터 셋은
        500000 -> 50만개
        1000000 -> 100만개
        1500000 -> 150만개 
      로 테스트를 진행했다. 

      이 경우 [인덱스 컬럼 + 인덱스 컬럼 + 인덱스 컬럼] 조합보다 

      [컬럼 + 컬럼 + 컬럼] 조합이 더 빠른 결과가 나왔다.

      일관된 데이터를 쭉 넣어서 인덱스가 효과를 못보는 것이 아닌가 해서 최대한 데이터들을 섞어서 넣었다.

      그랬더니 확실히 인덱스 컬럼이 빨랐다.

      즉, 인덱스는 데이터가 섞여 있을 때 효과를 발휘한다

      2)
      where 절 이후 모두 인덱스 컬럼일 경우에만 인덱스의 성능이 발휘된다.






