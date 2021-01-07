



    테스트 테이블
      +---------+---------+------+-----+---------+----------------+
      | Field   | Type    | Null | Key | Default | Extra          |
      +---------+---------+------+-----+---------+----------------+
      | id      | int(11) | NO   | PRI | NULL    | auto_increment |
      | value   | int(10) | YES  | MUL | NULL    |                |
      | value_2 | int(10) | YES  | MUL | NULL    |                |
      | value_3 | int(10) | YES  | MUL | NULL    |                |
      +---------+---------+------+-----+---------+----------------+

      +----------+
      | count(*) |
      +----------+
      |  2000000 |
      +----------+



    인덱스 컬럼 + 인덱스 컬럼 + 인덱스 컬럼

      | value   | int(10) | YES  | MUL | NULL    |                |
      | value_2 | int(10) | YES  | MUL | NULL    |                |
      | value_3 | int(10) | YES  | MUL | NULL    |                |

      select * from lab.index_test where value > 0 and value_2 > 0 and value_3 > 0;

      2000000 rows in set (0.94 sec)

      2000000 rows in set (0.92 sec)

      2000000 rows in set (0.91 sec)

    인덱스 컬럼 + 인덱스 컬럼 + 컬럼

      | value   | int(10) | YES  | MUL | NULL    |                |
      | value_2 | int(10) | YES  | MUL | NULL    |                |
      | value_3 | int(10) | YES  |     | NULL    |                |

      select * from lab.index_test where value > 0 and value_2 > 0 and value_3 > 0;

      2000000 rows in set (0.90 sec)
      2000000 rows in set (0.92 sec)
      2000000 rows in set (0.91 sec)

    인덱스 컬럼 + 컬럼 + 컬럼

      | value   | int(10) | YES  | MUL | NULL    |                |
      | value_2 | int(10) | YES  |     | NULL    |                |
      | value_3 | int(10) | YES  |     | NULL    |                |

      select * from lab.index_test where value > 0 and value_2 > 0 and value_3 > 0;

      2000000 rows in set (0.93 sec)

      2000000 rows in set (0.93 sec)

      2000000 rows in set (0.91 sec)

    컬럼 + 컬럼 + 컬럼

      | value   | int(10) | YES  |     | NULL    |                |
      | value_2 | int(10) | YES  |     | NULL    |                |
      | value_3 | int(10) | YES  |     | NULL    |                |

      2000000 rows in set (0.93 sec)

      2000000 rows in set (0.97 sec)

      2000000 rows in set (0.92 sec)

    컬럼 + 컬럼 + 컬럼(문자)

      | value   | int(10)     | YES  |     | NULL    |                |
      | value_2 | int(10)     | YES  |     | NULL    |                |
      | value_3 | varchar(10) | YES  |     | NULL    |                |

      2000000 rows in set (1.04 sec)

      2000000 rows in set (1.04 sec)

      2000000 rows in set (1.04 sec)

    결론
      숫자 컬럼은 인덱스를 설정하든 안하든 빠르다.

      문자 컬럼이 끼는 순간 느려진다
        최대한 숫자 where 절을 숫자 컬럼으로 구성하자( 테이블 짤 때 생각 )
