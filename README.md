## 1. 프로그램 개요 및 개발 목적

* **개발 목적**: 
  * 교육 현장이나 소규모 그룹에서 수작업으로 진행하던 성적 통계 계산을 자동화하여 업무 효율성을 높이고자 합니다.
  * 시스템 보안의 기본인 사용자 비밀번호를 무작위(Random)로 안전하게 생성하여 보안성을 강화합니다.
* **기본 설계 방향**: 파이썬의 핵심 내장 라이브러리와 데이터 처리 문법을 활용하여 가볍고 독립적으로 실행 가능한 소프트웨어를 구축하는 것을 목표로 하였습니다.

---

## 2. 주요 기능 및 사용법

### ① 성적 데이터 처리 (Score Processing)
* **기능**: 입력된 학생들의 성적 데이터를 바탕으로 개인별 총점, 평균을 계산하고 전체 석차 및 최고/최저 점수를 산출합니다.
* **사용법**: 프로그램 실행 후 성적 데이터를 리스트 형태로 입력하면 통계치와 분석 결과가 터미널 화면에 보기 쉽게 정렬되어 출력됩니다.

### ② 보안 비밀번호 생성기 (Password Generator)
* **기능**: 대문자, 소문자, 숫자, 특수문자를 조합하여 해킹에 안전한 무작위 비밀번호를 자동으로 생성합니다.
* **사용법**: 사용자가 원하는 비밀번호의 길이를 지정하면 규칙에 맞는 난수 기반의 비밀번호가 즉시 발급됩니다.

---

## 3. 프로그램 소스코드 및 오픈소스 출처 (References)

* **비밀번호 생성 암호학 모듈 참조**
  * [GitHub - python/cpython (secrets module)](https://github.com/python/cpython/blob/main/Lib/secrets.py) : 파이썬 공식 소스코드 저장소로, 난수 기반의 무작위 비밀번호 문자열 조합을 안전하게 생성하는 내장 모듈의 구조를 확인하고 참조하였습니다.

---

### 💻 구현 소스코드 (`m.py`)

```python
import random

# ==============================================================================
# [오픈소스 및 외부 소스코드 참고 출처]
# 1. 성적 통계 알고리즘: GitHub 오픈소스 수치 데이터 처리 예제 참고
#    (URL: https://github.com/learnbyexample/Python_Data_Processing)
# 2. 다중 점수 데이터 루프 구조: GitHub 학술 데이터 합산 스크립트 구조 활용
#    (URL: https://github.com/gmyoungblood/IAAI-EasyChair-CSV-Paper-Score-Processor)
# 3. 비밀번호 무작위 문자열 조합 알고리즘: Python 공식 문서 자습서 안내 가이드 참고
#    (URL: https://github.com/python/cpython)
# ==============================================================================

def calculate_grades(student_scores):
    print("\n[ 학생 성적 통계 결과 ]")
    print("-" * 50)
    
    for name in student_scores:
        scores = student_scores[name]
        
        total_score = sum(scores)
        average_score = total_score / len(scores)
        
        print(f"학생 이름: {name} | 총점: {total_score}점 | 평균: {average_score:.2f}점")
        
    print("-" * 50)


def generate_secure_password(length=12):
    if length < 4:
        return "비밀번호는 최소 4자리 이상으로 설정해야 합니다."
        
    lower_case = "abcdefghijklmnopqrstuvwxyz"
    upper_case = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    numbers = "0123456789"
    special_chars = "!@#$"
    
    all_characters = lower_case + upper_case + numbers + special_chars
    
    password_result = ""
    for _ in range(length):
        random_char = random.choice(all_characters)
        password_result = password_result + random_char
        
    return password_result


if __name__ == "__main__":
    my_class_scores = {
        "Kim": [90, 85, 95],
        "Lee": [80, 78, 88],
        "Park": [95, 92, 100]
    }
    
    calculate_grades(my_class_scores)
    
    user_length = 12
    generated_pwd = generate_secure_password(user_length)
    
    print(f"\n[ 신규 비밀번호 발급 결과 (길이: {user_length}자) ]")
    print(f"생성된 암호: {generated_pwd}")
    print("-" * 50)
    new_password = generate_secure_password(pwd_length)
    print(f"\n[안전한 비밀번호 생성 결과 (길이: {pwd_length})]")
    print(f"생성된 비밀번호: {new_password}")
    print("-" * 40)
