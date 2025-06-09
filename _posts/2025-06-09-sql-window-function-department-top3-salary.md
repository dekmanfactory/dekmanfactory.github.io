---
layout: single
title: "SQL 윈도우 함수로 부서별 급여 상위 3위 직원 찾기"
date: 2025-06-09
categories:
  - Database
  - SQL
  - Programming
tags:
  - SQL
  - Window Function
  - DENSE_RANK
  - Database Query
  - 데이터 분석
  - MySQL
sidebar:
  nav: "main"
toc: true
toc_sticky: true
---

다음 SQL 쿼리 중에서 윈도우 함수를 사용하여 각 부서별로 급여 상위 3위 안에 드는 직원을 찾는 가장 효율적인 방법은 무엇입니까? (단, 급여가 같은 경우에는 순위를 동일하게 처리합니다.)

① SELECT department, employee_id, salary FROM (SELECT department, employee_id, salary, DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) as rank_within_dept FROM employees) WHERE rank_within_dept <= 3;
② SELECT department, employee_id, salary FROM (SELECT department, employee_id, salary, RANK() OVER (PARTITION BY department ORDER BY salary DESC) as rank_within_dept FROM employees) WHERE rank_within_dept <= 3;
③ SELECT department, employee_id, salary FROM (SELECT department, employee_id, salary, ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as rank_within_dept FROM employees) WHERE rank_within_dept <= 3;
④ SELECT department, employee_id, salary FROM employees ORDER BY department, salary DESC LIMIT 3;

정답은 ①입니다.

① `DENSE_RANK()` 함수는 동일한 순위를 가지는 경우에도 다음 순위를 건너뛰지 않으므로, 급여가 같은 직원들이 있을 경우에도 상위 3위 안에 드는 모든 직원을 포함합니다.
② `RANK()` 함수는 동일한 순위를 가지는 경우 다음 순위를 건너뛰므로, 상위 3위 안에 드는 직원이 3명 이상일 경우 일부 직원이 누락될 수 있습니다.
③ `ROW_NUMBER()` 함수는 각 행에 고유한 순위를 부여하므로, 급여가 같은 직원이 있더라도 순위가 달라질 수 있습니다.
④ 윈도우 함수를 사용하지 않고 전체 데이터셋에서 상위 3명만 선택하므로, 부서별로 상위 3명을 찾는 데 적합하지 않습니다.
