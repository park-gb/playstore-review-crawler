# 파이썬 기반 구글 플레이 스토어 웹 크롤러 V.2.0.3
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Google Chrome](https://img.shields.io/badge/Google%20Chrome-4285F4?style=for-the-badge&logo=GoogleChrome&logoColor=white)

- 참고1) 개인 블로그 포스팅 ["구글 플레이 스토어 웹 크롤러 코드 Version2.0.3"](https://heytech.tistory.com/293)
- 참고2) 미국(US) 구글 플레이 스토어 웹 크롤러: ```dev_us``` branch
## 1. 업데이트 Log
### 2022-08-21
#### (1) find_element 구문 수정 
- 데이터 크롤링 섹션 내 16 line 수정 
- ```selenium 4.3.0``` 이후 버전 ```find_element_by_*``` 구문이 제거됨에 따른 구문 수정 
    - 변경 전: ```driver.find_element_by_xpath(all_review_button_xpath).click()```
    - 변경 후: ```driver.find_element(By.XPATH,all_review_button_xpath).click()```

#### (2) pipenv 가상환경 추가
- dependency 고려 위함

### 2022-07-19
#### (1) 크롬 드라이버 강제 종료 코드 추가
-  ```HTML 데이터 저장``` 섹션 전 단계에서  ```driver.quit()``` 코드 추가
- 메모리 누수 방지를 위해 실행된 모든 크롬 드라이버 강제 종료
- 정상 동작 확인

### 2022-06-22
#### (1) 웹  크롤링 함수 내 '리뷰 모두 보기' 버튼 path 수정
- AS-IS
  - ```all_review_button_xpath = '/html/body/c-wiz[2]/div/div/div[1]/div[2]/div/div[1]/c-wiz[3]/section/div/div/div[5]/div/div/button/span'```
- TO-BE (정상 동작 확인)
  - ```all_review_button_xpath = '/html/body/c-wiz[2]/div/div/div[1]/div[2]/div/div[1]/c-wiz[4]/section/div/div/div[5]/div/div/button/span'```

### 2022-01-27
#### (1) Modal Window 내 자동 무한 크롤링 추가
- 업데이트 배경
  - 구글 플레이 스토어 내 '모든 리뷰 보기' 페이지가 [Modal Window](https://ko.wikipedia.org/wiki/%EB%AA%A8%EB%8B%AC_%EC%9C%88%EB%8F%84)로 변경됨에 따라 기존 Crawler 사용 불가
#### (2) 코드 Refactoring

## 2. 주요 기능
- App 사용자 리뷰 데이터 수집
  - 리뷰 등록일
  - 작성자 닉네임
  - 리뷰 평점
  - 리뷰 내용

- Parsing 한 html 데이터 저장(`dataset/html_data.html`)
- 수집한 데이터는 데이터프레임 형태로 포맷팅(`dataset/review_dataset.csv`)
<img width="893" alt="res" src="https://user-images.githubusercontent.com/80144296/151114273-41166e1d-40cd-44ac-8c94-fdf01322c846.png">

## 3. 필수 초기세팅
### (1) 크롬 드라이버 설치
- 사용 중인 크롬 버전([확인방법](https://support.google.com/chrome/answer/95414?hl=ko&co=GENIE.Platform%3DDesktop))에 맞는 [크롬 드라이버 설치](https://chromedriver.chromium.org/downloads)
- 설치한 파일은 `src` 폴더의 상위에 위치
- 파일 확장자 이름 표기 여부에 따라 `src/crawler.ipynb` 파일 내 chrome driver 파일명 택 1
```python
# chrome_driver = '../chromedriver.exe' # 파일 확장자 이름 표기
chrome_driver = '../chromedriver' # 파일 확장자 이름 미표기
```

### (2) 앱 URL 세팅
- [구글 플레이 스토어](https://play.google.com/store/apps)에서 수집할 App 검색 후 App 선택
- App 소개 웹 페이지 URL 복사(아래 스크린샷 내 빨간 박스)
<img width="800" alt="스크린샷 2021-10-01 오후 12 09 59" src="https://user-images.githubusercontent.com/80144296/135559627-356f1d9d-eac9-425d-aad9-e60403d8baba.png">

- `src/crawler.ipynb` 파일 내 App url 수정
```python
url = 'https://play.google.com/store/apps/details?id=com.github.android' # 예시: Github App 주소
```
### (3) pipenv 가상환경 설치
- 1) [[Python] pipenv 등장배경, 설치, 패키지 관리 방법](https://heytech.tistory.com/320)
- 2) [[Python] Jupyter Notebook(Lab)에 가상환경 커널 추가 방법](https://heytech.tistory.com/324)


### (4) 파이썬 패키지 설치
- pipenv 설치 및  ```master branch``` 클론 후 아래 명령어 실행
```python
$ pipenv install
```
- python ==3.8
- pandas==1.4.3
- selenium==4.4.3
- beautifulsoup4==4.11.1

## 4. 전체 파일구조
``` bash
├─playstore-review-crawler
│ Pipfile.lock
│ Pipfile.txt
│ README.md
│ chromedriver
│  ├─src
│  │      crawler.ipynb
│  │      dataHTML.html
│  └─dataset
│         review_dataset.csv
```

## 5. 실행 결과
![crawler_park-gb](https://user-images.githubusercontent.com/80144296/151113992-ee768495-84cd-45e7-a30c-6b1f90106096.gif)

## 📝 License
```
MIT License

Copyright (c) 2022 Gyeongbin Park

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
``
