
	테스트 테이블
		+------------+--------------+------+-----+---------+----------------+
		| Field      | Type         | Null | Key | Default | Extra          |
		+------------+--------------+------+-----+---------+----------------+
		| id         | int(11)      | NO   | PRI | NULL    | auto_increment |
		| name       | varchar(100) | NO   |     | NULL    |                |
		| team_code  | varchar(10)  | YES  |     | NULL    |                |
		| addr       | varchar(100) | YES  |     | NULL    |                |
		| salary     | int(10)      | NO   | MUL | NULL    |                |
		| job        | varchar(20)  | YES  |     | NULL    |                |
		| commission | int(7)       | YES  |     | NULL    |                |
		| gender     | varchar(2)   | YES  |     | NULL    |                |
		| hire_date  | date         | YES  |     | NULL    |                |
		| out_date   | varchar(45)  | YES  |     | NULL    |                |
		+------------+--------------+------+-----+---------+----------------+

		+----------+
		| count(*) |
		+----------+
		|  1417371 |
		+----------+


	------------------------------------------------------------------------------------------------------

	컬럼 : 숫자
	인덱스 : O

		비교 관계
			일치)
				SELECT * FROM member where salary = 3000000;

				317361 rows in set (0.51 sec)

				317361 rows in set (0.51 sec)

				317361 rows in set (0.51 sec)

			불일치)
				SELECT * FROM member where salary = '3000000';

				317361 rows in set (0.51 sec)

				317361 rows in set (0.51 sec)

				317361 rows in set (0.51 sec)



		대소 관계
			일치)
				SELECT * FROM member where salary > 2000000;

				1317361 rows in set (1.29 sec)

				1317361 rows in set (1.29 sec)

				1317361 rows in set (1.29 sec)

			불일치)
				SELECT * FROM member where salary >'2000000';

				1317361 rows in set (1.30 sec)

				1317361 rows in set (1.29 sec)

				1317361 rows in set (1.29 sec)


	컬럼 : 숫자
	인덱스 : X
		비교 관계
			일치)
				SELECT * FROM lab.member where commission = 2000000;

				317361 rows in set (0.71 sec)

				317361 rows in set (0.71 sec)

				317361 rows in set (0.72 sec)


			불일치)
				SELECT * FROM lab.member where commission = '2000000';

				317361 rows in set (0.71 sec)

				317361 rows in set (0.72 sec)

				317361 rows in set (0.72 sec)


	결과
		숫자 컬럼에서는 문자 또는 숫자 둘 중 어느 것으로 대입해서 크게 영향을 끼치진 않는다

	------------------------------------------------------------------------------------------------------

	salary -> varchar(10)
	commision -> varchar(7)


	컬럼 : 문자
	인덱스 : O
		비교 관계
			일치)
				SELECT * FROM lab.member where salary = '3000000';

				317361 rows in set (0.56 sec)

				317361 rows in set (0.50 sec)

				317361 rows in set (0.51 sec)


			불일치)
				SELECT * FROM lab.member where salary = 3000000;

				317361 rows in set (0.80 sec)

				317361 rows in set (0.78 sec)

				317361 rows in set (0.77 sec)

	컬럼 : 문자
	인덱스 : X 
		비교 관계
			일치)
				SELECT * FROM lab.member where commission = '2000000';

				317361 rows in set (0.73 sec)

				317361 rows in set (0.72 sec)

				317361 rows in set (0.73 sec)

			불일치)
				317361 rows in set (0.77 sec)

				317361 rows in set (0.78 sec)

				317361 rows in set (0.77 sec)

	결과
		인덱스가 있는 컬럼일 경우 영향이 크다
			인덱스 X)
				타입 일치 -> 평균 속도 : 약 0.72 sec
				타입 불일치 -> 평균 속도 : 약 0.77 sec
				증감율 : 약 7%

			인덱스 0)
				타입 일치 -> 평균 속도 : 약 0.52 sec
				타입 불일치 -> 평균 속도 : 약 0.78 sec
				증감율 : 약 50 %






	최종 결론
		어떤 컬럼이냐에 따라 다르겠지만, 컬럼과 대입하는 데이터 타입이 다른 경우 성능에 영향을 끼친다.
