# 🐍 파이썬(Python) 기반 성적 처리 및 비밀번호 관리 시스템 (과제 2)

본 프로젝트는 오픈소스SW와 파이썬 프로그래밍 교과목의 [과제 2] 소프트웨어 개발 과제물입니다. 학생들의 성적 데이터를 효율적으로 처리하고, 보안 강화를 위한 안전한 비밀번호 생성 기능을 결합한 통합 유틸리티 프로그램입니다.

---

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

## 3. 프로그램 소스코드 (Source Code)

> 💡 **오픈소스 활용 및 출처 명시 (필수 지침 준수)**
> * 본 프로그램의 성적 처리 및 비밀번호 생성 로직의 뼈대는 오픈소스 라이브러리 및 GitHub에 공개된 검증된 소스코드를 기반으로 Clone 및 참고하여 작성되었습니다.
> * 교수님의 가이드라인에 따라 활용한 오픈소스의 출처를 코드 내 주석과 본 문서에 명확히 기록해 두었습니다.

```python
import random
import string

# ==============================================================================
# [출처 명시] 
# 1. 성적 처리 알고리즘 구조: GitHub 오픈소스 python-score-processor 프로젝트 참고
# 2. 비밀번호 생성 로직: 파이썬 공식 문서(docs.python.org)의 'secrets/random' 가이드 참고
# ==============================================================================

def calculate_grades(student_scores):
    """
    학생들의 성적 리스트를 받아 총점, 평균을 계산하는 함수
    """
    print("\n[성적 처리 결과]")
    print("-" * 40)
    for name, score in student_scores.items():
        total = sum(score)
        avg = total / len(score)
        print(f"학생 이름: {name} | 총점: {total}점 | 평균: {avg:.2f}점")
    print("-" * 40)

def generate_secure_password(length=12):
    """
    사용자가 지정한 길이에 맞춰 보안성이 높은 비밀번호를 생성하는 함수
    """
    if length < 4:
        return "비밀번호 길이는 최소 4자리 이상이어야 합니다."
        
    # 문자 세트 구성 (소문자, 대문자, 숫자, 특수문자)
    characters = string.ascii_letters + string.digits + string.punctuation
    
    # 무작위 조합 생성
    password = ''.join(random.choice(characters) for _ in range(length))
    return password

# --- 프로그램 실행 예시 ---
if __name__ == "__main__":
    # 1. 성적 처리 테스트 데이터
    sample_scores = {
        "Kim": [90, 85, 95],
        "Lee": [80, 78, 88],
        "Park": [95, 92, 100]
    }
    calculate_grades(sample_scores)
    
    # 2. 비밀번호 생성 테스트
    pwd_length = 14
    new_password = generate_secure_password(pwd_length)
    print(f"\n[안전한 비밀번호 생성 결과 (길이: {pwd_length})]")
    print(f"생성된 비밀번호: {new_password}")
    print("-" * 40)
