# 250311_image_scraping_python
파이선(주피터노트북, colab) 을 이용한 이미지 스크래핑 코드입니다!

## 파이선 웹 스크래핑

---

```python
!pip install bing-image-downloader
# 코랩이 인터넷 프로그램이라 이미지 다운로더를 다운받는다고 생각하면 된다
```

이미지 다운로더를 갖고온다고 생각하자

```python
# bing_image_downloader 모듈에서 downloader를 가져옴
from bing_image_downloader import downloader 

# pathlib 모듈에서 Path를 가져옴
from pathlib import Path 

def download_images(keyword, num_images, file_name):

		# 이미지를 저장할 폴더 이름
    output_directory = "can" 
    
    # 이미지 다운로드
    downloader.download(keyword, limit=num_images, output_dir=output_directory, adult_filter_off=True, force_replace=False, timeout=60)

		# 이미지 저장 폴더의 경로
    root = Path().cwd() / output_directory 

		# 폴더 내 모든 파일 가져오기
    downloaded_files = list(root.glob("*.*")) 

		# 다운로드된 각 파일에 대해 반복
    for i, file in enumerate(downloaded_files): 

        extension = file.suffix # 파일 확장자

        new_file_name = f"{file_name}{i+1}{extension}" # 새로운 파일 이름

        new_file_path = root / new_file_name # 새로운 파일 경로

        file.rename(new_file_path) # 파일 이름 변경

```

다운로드 이미지라는 함수에 폴더 만들고,

이미지 다운로드 하고

경로지정, 폴더 내 파일, 그리고 반복해주면 된다!

이름 설정도 할 수 있다

**사용 예시**

```python
# 이미지 검색 키워드
keyword = "포카리캔" 

# 다운로드할 이미지 수
num_images = 100 

# 파일 이름
file_name = "포카리" 
```

이렇게 키워드(검색키워드 넣고 파일 다운로드!)

**구글 드라이브 연동**

```python
from google.colab import drive
drive.mount('/content/drive') 

# 이미지 다운로드
download_images(keyword, num_images, file_name) 
```

그러면 파일이 막 다운로드된다!

**파일 압축해서 한번에 다운하기**

```python
import shutil

def compress_folder(folder_path, output_path):
    shutil.make_archive(output_path, 'zip', folder_path)

# 이미지 저장 폴더 압축
folder_path = "/content/can/포카리캔" # 저장경로
output_path = "포카리"                # 파일이름
compress_folder(folder_path, output_path)
```

그냥 다운로드는 안돼서.. 파일 압축해서 다운해야한다!

![image.png](attachment:da0b464d-b643-4c52-a52c-83025fea2c9d:image.png)

이렇게 zip을 해줘야 다운로드 가능

코드 보고 집에 가서 공부해봅시다!
