# 파이썬 기반 구글 플레이 스토어 웹 크롤러
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Google Chrome](https://img.shields.io/badge/Google%20Chrome-4285F4?style=for-the-badge&logo=GoogleChrome&logoColor=white)

## 1. 주요 기능
- App 사용자 리뷰 데이터 수집
  - 리뷰 등록일
  - 작성자 닉네임
  - 리뷰 내용
  - 리뷰 평점
- Parsing 한 html 데이터 저장(`./dataset/html_data.html`)
- 수집한 데이터는 데이터프레임 형태로 포맷팅(`./dataset/review_dataset.csv`)
<img width="829" alt="스크린샷 2021-10-01 오전 11 17 06" src="https://user-images.githubusercontent.com/80144296/135555380-d074d1ee-2ff6-43e3-b39e-b0ab9103c8de.png">

## 2. 사용 전 필수 초기세팅 절차
### (1) 크롬 드라이버 설치
- 사용 중인 크롬 버전([확인방법](https://support.google.com/chrome/answer/95414?hl=ko&co=GENIE.Platform%3DDesktop))에 맞는 [크롬 드라이버 설치](https://chromedriver.chromium.org/downloads)
- 설치한 파일은 `src` 폴더의 상위에 위치
- 파일 확장자 이름 표기 여부에 따라 `./src/crawler.ipynb` 파일 내 chrome driver 파일명 택 1
```python
# chrome_driver = '../chromedriver.exe' # 파일 확장자 이름 표기
chrome_driver = '../chromedriver' # 파일 확장자 이름 미표기
```

### (2) 앱 URL 세팅
- [구글 플레이 스토어](https://play.google.com/store/apps)에서 수집할 App 검색 후 App 선택
- App 소개 웹 페이지 URL 복사(아래 스크린샷 내 빨간 박스)
<img width="800" alt="스크린샷 2021-10-01 오후 12 09 59" src="https://user-images.githubusercontent.com/80144296/135559627-356f1d9d-eac9-425d-aad9-e60403d8baba.png">

- `./src/crawler.ipynb` 파일 내 App url 수정
```python
url = 'https://play.google.com/store/apps/details?id=com.github.android' # 예시: Github App 주소
```

### (3) 파이썬 패키지 설치
```python
$ pip install beautifulsoup4
$ pip install selenium
$ pip install tqdm
$ pip install pandas
```
- [beatuiful soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/): HTML/XML 문서 parsing
- [selenium](https://selenium-python.readthedocs.io/installation.html): 브라우저 동작 자동 제어
- [pandas](https://pandas.pydata.org/): 데이터 분석 라이브러리
- [tqdm](https://pypi.org/project/tqdm/#installation): 작업 프로세스 바(progress bar) 시각화

## 3. 전체 파일구조
``` bash
├─Github
│  │  README.md
│  │  chromedriver
│  ├─src
│  │      crawler.ipynb
│  └─dataset
│          review_dataset.csv
│          html_data.html
