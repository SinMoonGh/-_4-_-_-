# 멋사 이력서 입니다.

## 목차

- [소개](#소개)
- [기술 스택](#기술-스택)
- [프로젝트 경험](#프로젝트-경험)
- [교육](#교육)

## 소개

안녕하세요. 멋사에서 파이썬 백엔드 교육 받고 있는 Myeong Hoon Sin입니다.

## 기술 스택
- **프로그래밍 언어**: Python
- **웹 프레임워크**: Django
- **데이터베이스**: PostgreSQL
- **기타 기술**: Docker, AWS


## 프로젝트 경험

- **링크**: [https://github.com/choi-jyoon/franding.git](https://github.com/choi-jyoon/franding.git)
- **설명**: 향수 입문자들을 위한 향수 추천 서비스와 무료 시향지 제공 서비스로 다른 사이트와 차별화를 둔 향수 사이트
- **기술 스택**: python, django, postgreSQL, Docker, Aws, redis
- **역할**:

#### 1. 장바구니 기능
- 장바구니 기능에서 상품을 삭제할 시 리로딩이 되면서 뒤로 가기 버튼을 눌러도 이전 페이지로 돌아가지 않는 문제 직면.

- Ajax를 사용하여 비동기적으로 처리(리로딩 되면서 페이지가 새로 고침 되어야 상품이 삭제처리 되는 것이 아니라 삭제 버튼을 누름과 동시에 상품이 삭제되는 기능을 구현하고 싶었음)하여 뒤로 가기 클릭 시 페이지가 돌아가지 않는 문제를 해결하고 편의성을 향상시키고 싶었습니다.

- 구상한 내용대로 구현하는 것은 좋았으나 '진정 사용자의 편의성을 개선시켰나?' 에 대한 의구심이 남았습니다.

#### 2. 장바구니 배지
- 장바구니에 상품을 담았을 때 장바구니 아이콘에 상품 수량을 표시해주는 기능 개발.

- 기능 명세서를 보고 처음에 떠올린 생각은 데이터베이스에 값을 저장하고 서버에서 호출하는 방법이었음. 하지만 장바구니 상품 수량을 구할 수 있는 값들은 이미 데이터베이스에 저장이 되어있는 데다가 데이터 낭비라는 생각이 들어서 방향을 바꾸게 되었습니다.
Db에서 수량을 구하는데 필요한 값들을 가져와서 서버에서 연산하고, 그 값을 템플릿으로 전송해주는 방식을 선택하였습니다.
- 여기서 문제에 직면했습니다. 장바구니에 상품을 담을 때는 값이 존재하지만 페이지 이동 시에 값이 없어지는 문제가 생겼습니다.
기존의 방법으로는 페이지 이동 시 값이 없어지는 문제를 해결할 수 가 없어서 쿠키에 저장할 지, 아니면 그냥 db에 저장할 지, 로컬 스토리지에 저장할 지에 대해서 고민하다가 3번 째 방법을 선택하였습니다.
일단 저장, 호출, 삭제가 코드 1줄만 치면 되기 때문에 매우 간편하다고 생각했고, 이 상황에 매우 적합한 방식이라고 생각이 들었습니다.

- 하지만 서버에서 받아온 값을 로컬 스토리지에 저장한 후 웹페이지가 새로 고침 될 때 값이 1증가 되어야 하는데 실시간으로 반영되지 않는 문제가 생겼다. Ajax를 사용해도 문제가 해결되지 않았고(실은 ajax가 비동기 통신을 한다는 것만 알지 어떻게 서버와 통신하고, 값을 서로 주고 받는 지에 대해서는 무지하다)문제 해결과정에서 많은 시간이 소모되어 포기하고 다른 작업에 들어갔습니다.

- 포기하게 된 가장 결정적인 이유라고 생각되는 부분은 나의 고집이었다. 개발을 하다가 내가 구상하고 있는 방법으로는 도저히 해결이 안 될 때 이 방법을 버리고 현실적인 대안(당장 문제가 해결될 확률이 가장 높은 방법)을 선택해야 되는데 이것보다 더 좋은 방법이 있을 거라고 검색하고, 기능에 대한 로직을 제대로 구성하지도 않은 채 무턱대고 코드만 입력한 결과 많은 시간을 오류를 해결하는데 시간을 써야 됐고 그 결과는 실패였습니다.

#### 3. 상품 추천
- 고객이 자신이 고른 상품을 장바구니에 담고 결제를 한다거나 장바구니에 담은 상품 목록을 확인하기 위해서 장바구니 페이지로 이동했을 경우 볼 수 밖에 없는 위치에 우리의 대표 상품을 홍보하기 위해서 기능을 개발하게 되었습니다.

- 기존에 만들었던(고객이 가장 많이 구매한 상품 추천) 추천 기능을 갈아엎고, 검색-증강 생성(rag)을 이용하였습니다.
먼저 향수 데이터베이스에 있는 모든 데이터를  llm모델이 참조하게 하여 응답을 요청 받을 때 제공한 정보를 토대로 응답할 수 있도록 유도했습니다. 또한 프롬프트를 입력하여 내가 얻고자 하는 응답을 구체적으로 받을 수 있도록 했습니다.

- 입력한 프롬프트 : 
데이터베이스에서 많은 사람이 구매한 제품을 추천해주세요.
데이터베이스에서 별점이 많은 상품을 추천해주세요.
데이터베이스에서 가격이 높은 상품을 추천해주세요.
데이터베이스에서 리뷰가 좋은 제품을 추천해주세요.
상품을 3개 이상 추천해주세요.

- 상품 추천 기능을 구현하면서 들었던 생각은 왜 이 상품을 추천했는가? 어떤 정보가 반영되었고, 어떤 정보가 반영되지 않았는가? 실제로 ai가 추천한 상품은 고객들의 니즈를 끌어올릴 수 있는가? 같은 의문과 더불어 검증되지 않은 결과 만큼 위험한 것 없지 않을까? 라는 의구심이 들었습니다. 실제로 데이터 수집하는 과정 그리고 수집한 데이터를 처리하는 것과 회사의 수익으로 이어지게 하기 위해서 어떤 공부를 해야 될 지에 대한 부분을 고민하게 되었습니다.

#### 4. Q&A 게시판
- 고객의 요청사항과 질문사항들을 실시간으로 반영하기 위해서 Q&A게시판을 개발하였습니다.

- 상품 상세 페이지에서 문의하기 버튼을 누르면 고객이 문의할 수 있는 폼을 작성할 수 있도록 구성했다. 폼을 작성하면 판매자가 질문을 확인하고 답변을 달 수 있으며, 고객은 자신이 질문한 질문 목록을 확인하고 답변이 달린 질문은 버튼 색깔을 변경하여 답변이 달린 질문이라는 것을 한 눈에 볼 수 있게 개선, 사용 편의성을 향상시키려고 노력하였습니다.

- 초반 구상 단계에서 머릿 속으로만 구상한 내용을 그대로 코드로 옮겨 치는 실수를 하는 바람에 중간에 로직이 엄청 꼬여서 헤맸었다. 어디까지가 올바는 방향이고, 어디서부터 잘못된 방향을 선택했는지 찾을 수 없을 뿐더러 두 곳에서 서로 다른 데이터를 하나의 서버에 전송 및 요청하는 어이없는 실수도 저지르고 말았다. 분명 데이터는 제대로 보냈는데 서버에서 값이 전송되지 않으니 오류의 원인이 뭔지도 모른 채 문제가 없는 코드만 수정 및 디버깅을 반복했습니다. 

- 문제 해결의 열쇠는 강사님께 얻었는데 다시 처음부터 새로 구상을 하는 것이다. 이미 내가 생각했던 방법이었어도 하나하나 짚어가다 보면 오류가 보인다는 것이었습니다.
새로 구상한 방법은 아주 간단했습니다.
1. 특정 고객이 질문을 작성한다.
2. 일단 모든 고객의 질문들을 보여준다.
3. 특정 고객의 질문만 보여준다.

그때 구상했던 메모 : 
1. 상품 상세페이지에서 1대1문의하기 버튼을 누른다

2. 상품에 관한 질문을 적는다.

3. 질문 내용은 마이페이지에서 확인 가능

4. 판매자가 답변을 입력하면 읽지 않은 답변이 있다고 기재

5. q&a 에서 빈화면 나오게 하고

6. 전체 q&a 가 나오도록 하고

7. 특정 사람에 대해서 작성한 q&a가 나오게 하면 된다.

8. 각 질문마다 판매자의 답변이 보이도록 출력
---
        상품 , 제목

        -답변 확인-  

        Click 시
        
        질문 내용

        답변 내용

        도움이 됐어요 | 아쉬워요 -> 투표 후 버튼 비활성화

        페이지네이션

---

- 오류와 싸우다 처음부터 다시 한 구상은 매우 간단했다. 폼을 받아서 출력해주고, 분류하는 게 전부였으니까 말이다.
이전에는 모든 질문 목록을 출력하는 부분을 건너뛰고 특정 고객의 질문을 받아서 판매자 페이지와 고객페이지로 동시에 보내는 방법을 고민하다 막혔었습니다. 
이 경험을 통해서 아무리 작은 기능이라도 하나하나 로직을 세워야 한다는 것과 해결하지 못하는 오류가 있을 땐 처음부터 다시 로직을 구성해 보는 것이 필요하다는 것을 깨달았습니다.

#### 5. Q&A 검색 기능

- 수많은 고객이 질문을 쏟아낸다면 판매자가 그 수많은 질문들 중에 특정한 어느 하나를 찾을 수 있을까? 에 대한 고민에서 시작되었다. 정렬 기능이 있긴 하지만 다소 부족해 보였고, 메인 검색란이 있지만 게시판 검색엔 쓸 수 가 없었기 때문에 게시판 전용 검색 기능이 필요하다는 생각이 들었다. 따라서 이러한 이유들로 Q&A 검색 기능을 추가하였습니다.

- 먼저 강사님께서 강의하신 내용 중에 검색에 대한 강의안이 있다는 것을 떠올렸다. 제목은 'Vector DB를 이용한 자연어 검색 API'이고, 구현 순서를 설명하면 먼저 검색할 데이터(질문 리스트)를 csv파일로 만든다. 그리고 langchain의 HuggingFaceEmbeddings를 사용해 모델을 초기화 및 Chroma를 이용하여 벡터 저장소를 생성하고, similarity_search 메서드에 검색어를 넣어주면 입력 쿼리와 저장된 데이터(질문 리스트)들 사이의 유사도를 계산하고, 가장 유사한 결과를 반환해 줍니다. 
- 여기서 문제는 Chroma.from_texts메서드의 texts(
texts: List[str], embedding: Embeddings | None = None,
)에 해당된 값만 검색어와 비교해서 검색어와 유사한 결과를 반환해준다는 것입니다.
예를 들어, 도서 이름 : 삼남매 / 출판 년도 : 2021년 / 분류 : 과학 이라는 book 데이터가 있을 때 도서 이름으로 검색하고 싶다면 texts 값에 '삼남매' 라고 할당하면 된다. 그런데 만약 분류로 검색하고 싶다면? 
- Texts 값에 '삼남매' 밖에 없는데 검색어로 과학이라고 입력하면 과학이라는 단어와 유사한 도서 이름을 조회한다. 따라서 분류로 조회하고 싶다면 texts 값에 "삼남매+' ' + 과학" 이라는 문자열을 구성해야 합니다.
- 밑에는 id, 제목, 질문 내용, 작성 일자 로 분류된 값들을 하나씩 조회해서 text_list에 저장한 코드입니다.

```bash
def vector_store_texts(data_file):
    id = data_file()['id'].tolist()
    title = data_file()['title'].tolist()
    content = data_file()['content'].tolist()
    created_at = data_file()['created_at'].tolist()
    text_list = []
    for i, x, y, z in zip(id, title, content, created_at):
        str_i = str(i)
        texts = str_i + ", " + x + ", " + y + ", " + z
        text_list.append(texts)
    return text_list
```

- data_file은 질문 리스트(csv)이고, text_list 값은 ['1', '삼남매', '2021년', '과학'], ['2', …] 이런 식으로 저장됩니다.  

전체 소스 코드
```bash

from fastapi import FastAPI, HTTPException
import pandas as pd
from langchain_community.embeddings.sentence_transformer import SentenceTransformerEmbeddings
from langchain_chroma import Chroma
from langchain_huggingface import HuggingFaceEmbeddings
import uvicorn

# 데이터 로드
def load_data():
    qna_csv = pd.read_csv('my_langchain/csv_file/QnA.csv')
    return qna_csv

# 임베딩 모델 초기화
def init_model():
    # sbert = SentenceTransformerEmbeddings(model_name='jhgan/ko-sroberta-multitask')
    sbert = HuggingFaceEmbeddings(model_name='jhgan/ko-sroberta-multitask')
    return sbert 

# data_file()['title'].tolist()+data_file()['content'].tolist() 어떻게?
def vector_store_texts(data_file):
    id = data_file()['id'].tolist()
    title = data_file()['title'].tolist()
    content = data_file()['content'].tolist()
    created_at = data_file()['created_at'].tolist()
    text_list = []
    for i, x, y, z in zip(id, title, content, created_at):
        str_i = str(i)
        texts = str_i + ", " + x + ", " + y + ", " + z
        text_list.append(texts)
    return text_list

# 벡터 저장소 생성
def init_vector_store(data_file, sbert):
         vector_store = Chroma.from_texts(
        texts = vector_store_texts(data_file),
        embedding=sbert(),
    )
    return vector_store

def search_question(query):
    vector_store = init_vector_store(load_data, init_model)
    results = vector_store.similarity_search(query=query, k=10)  # 상위 3개 결과 반환
    return {"query": query, "results": results}
```


- 기능을 구현하면서 ai의 응답을 어떻게 처리해야 내가 사용할 수 있는 형태로 만들 수 있을까? 에 대한 고민을 많이 할 수 밖에 없었다. 실제로 응답은 매우 훌륭했지만 서비스에 적용하지 못하면 아무 쓸모가 없었기 때문이다. 나의 해답은 text_list에 id 값을 넣는 거였고, 리스트에서 id값만 필터링해서 적용했습니다.

#### 6. redis

- Ai를 이용해서 만든 추천 기능과 검색 기능이 작동하는 데에 많은 소요시간이 걸렸다. 어떻게 해야 소요시간을 줄일 수 있을까 생각하다가 응답 값을 받으면 그 값을 캐시에 저장해 놨다가 다음에 동일한 요청이 있을 경우 캐시에 저장되어 있던 값을 반환하면 속도가 향상되지 않을까? 에서 시작되었습니다.

- 먼저 강의안에 올라와 있는 장고가 제공해주는(내 컴퓨터 메모리에 저장) 캐시 기능을 이용하였습니다. 하지만 메모리에 저장할 때의 문제는 서버가 꺼지면 캐시에 있는 데이터가 전부 지워진다는 것입니다.
서버가 꺼져도 캐시에 저장되어 있는 데이터가 지워지지 않는 방법을 찾다가 redis 서버를 이용하면 구현이 가능하다는 것을 알게 되었습니다. 
- 구현 단계는 aws ec2 서버 가동 -> docker를 설치 -> redis를 설치 -> redis이미지로 redis-container를 생성.


#### 7. deploy.yml file

- ci/cd를 실습하고 싶어서 만든 파일입니다. Franding 프로젝트 배포에 필요한 모든 작업, 폴더 생성, 라이브러리 설치, 이미지 & 컨테이너 생성까지 이 파일 하나로 해결하고 싶었습니다.

소스코드 : 

```bash
name: Deploy to EC2
# main branch push 하기
on:
  push:
    branches:
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2
    - name: Install SSH client
      run: sudo apt-get install -y openssh-client
    - name: Add SSH key
      run: |
        mkdir -p ~/.ssh
        echo "${{ secrets.EC2_SSH_KEY }}" > ~/.ssh/franding.pem
        chmod 600 ~/.ssh/franding.pem
  
    - name: Add EC2 host to known_hosts
      run: |
        ssh-keyscan -H ${{ secrets.EC2_HOST }} >> ~/.ssh/known_hosts
    
    - name: Deploy to EC2 and install Docker
      env:
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        AWS_REGION: 'ap-northeast-2'
        EC2_INSTANCE_ID: ${{ secrets.EC2_INSTANCE_ID }}
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          sudo apt-get update -y
          sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
          curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
          sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
          sudo apt-get update -y
          sudo apt-get install -y docker-ce
          sudo usermod -aG docker $USER
          sudo systemctl enable docker
          sudo systemctl start docker
          docker --version          
        EOF
    - name: git clone 
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} '
          if [ -d "/home/ubuntu/2024_franding_project_-" ]; then
            echo "Directory exists. Pulling latest changes..."
            cd /home/ubuntu/2024_franding_project_-
            git pull
          else
            echo "Directory does not exist. Cloning repository..."
            git clone https://github.com/SinMoonGh/2024_franding_project_-.git
          fi'
    - name: franding_django .env 파일 생성하기
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          # .env 파일 생성
          cat <<EOT > ~/2024_franding_project_-/.env
          DJANGO_SECRET_KEY=${{ secrets.DJANGO_SECRET_KEY }}
          DB_PASSWORD=${{ secrets.DB_PASSWORD }}
          DB_PORT=${{ secrets.DB_PORT }}
          DB_NAME=${{ secrets.DB_NAME }}
          DB_HOST=${{ secrets.DB_HOST }}
          admin_key=${{ secrets.ADMIN_KEY }}
          OPENAI_API_KEY=${{ secrets.OPENAI_API_KEY }}
          SECRET_KEY=${{ secrets.SECRET_KEY }}
          KAKAO_CLIENT_ID=${{ secrets.KAKAO_CLIENT_ID }}
          KAKAO_KEY=${{ secrets.KAKAO_KEY }}
          GOOGLE_CLIENT_ID=${{ secrets.GOOGLE_CLIENT_ID }}
          GOOGLE_KEY=${{ secrets.GOOGLE_KEY }}
          EMAIL_HOST_USER=${{ secrets.EMAIL_HOST_USER }}
          EMAIL_PASSWORD=${{ secrets.EMAIL_PASSWORD }}
          AWS_ACCESS_KEY=${{ secrets.AWS_ACCESS_KEY }}
          AWS_SECRET_ACCESS_KEY=${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_BUCKET_NAME=${{ secrets.AWS_BUCKET_NAME }}
          AWS_S3_REGION_NAME=${{ secrets.AWS_S3_REGION_NAME }}
        EOF             
    - name: franding 네트워크 생성하기
      run: |
          ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} '
            # Create a custom network
            if sudo docker network inspect franding-network > /dev/null 2>&1; then
              echo "Docker network already exists. Skipping creation."
            else
              sudo docker network create franding-network
            fi'    
    - name: franding_django Dockerfile 생성하기
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          # Copy Dockerfile and necessary files
          cat <<EOT > ~/2024_franding_project_-/Dockerfile
          # Base image
          FROM python:3.10-slim
          # Set environment variables
          ENV PYTHONDONTWRITEBYTECODE 1
          ENV PYTHONUNBUFFERED 1
          # Set work directory
          WORKDIR /app
          # Install dependencies
          COPY requirements.txt /app/
          RUN pip install --upgrade pip
          RUN pip install -r requirements.txt
          # Copy project
          COPY . /app/
          # Expose the port the app runs on
          EXPOSE 8000
          # Run the application
          CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
        EOF
    
    - name: franding_django 이미지 빌드하기
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          cd ~/2024_franding_project_-
          # franding_django 이미지가 이미 존재하는지 확인
          if sudo docker image inspect franding-django-img > /dev/null 2>&1; then
            echo "Docker image already exists. Skipping build."
          else
            sudo docker build -t franding-django-img:latest .  
          fi        
        EOF

    - name: franding_django 컨테이너 실행하기
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          # Stop existing container if running
          sudo docker stop franding-container || true
          # Remove existing container if exists
          sudo docker rm franding-container || true
          # Run Docker container
          sudo docker run -d -p 8000:8000 --name franding-container -v /home/ubuntu/2024_franding_project_-:/app --network franding-network franding-django-img:latest
        EOF
    - name: nginx.conf 파일 생성하기
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          # Copy nginx.conf and necessary files
          cat <<EOT > ~/nginx/nginx.conf
          server {
              listen 80;
              location / {
                  proxy_pass http://franding-container:8000;
                  proxy_set_header Host $host;
                  proxy_set_header X-Real-IP $remote_addr;
                  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                  proxy_set_header X-Forwarded-Proto $scheme;
              }
          }
          EOT  
        EOF
    - name: nginx Dockerfile 생성하기
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          # nginx 폴더 생성
          mkdir -p ~/nginx
          # Copy Dockerfile and necessary files
          cat <<EOT > ~/nginx/Dockerfile
          # 베이스 이미지로 Nginx 사용
          FROM nginx:latest
          # Nginx 설정 파일 복사 (옵션)
          # 만약 커스텀 설정 파일을 사용하려면, 아래와 같이 설정 파일을 복사합니다.
          COPY nginx.conf /etc/nginx/conf.d/default.conf
          # 기본 HTML 파일 복사 (옵션)
          # 만약 커스텀 웹 페이지를 사용하려면, 아래와 같이 파일을 복사합니다.
          # COPY index.html /usr/share/nginx/html/index.html
          # 포트 80 노출
          EXPOSE 80
        EOF
    - name: nginx 이미지 빌드하기
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          cd ~/nginx
          # nginx 이미지가 이미 존재하는지 확인
          if sudo docker image inspect franding-nginx-img > /dev/null 2>&1; then
            echo "Docker image already exists. Skipping build."
          else
            sudo docker build -t franding-nginx-img:latest .  
          fi        
        EOF
    - name: nginx 컨테이너 실행하기
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
          # Stop existing container if running
          sudo docker stop franding-nginx-container || true
          # Remove existing container if exists
          sudo docker rm franding-nginx-container || true
          # Run Docker container
          sudo docker run -d -p 80:80 --name franding-nginx-container --network franding-network franding-nginx-img
        EOF
    - name: Verify Redis is running
      run: |
        ssh -i ~/.ssh/franding.pem ubuntu@${{ secrets.EC2_HOST }} << 'EOF' 
          # Pull Redis image
          sudo docker pull redis
          # Stop existing Redis container if running
          sudo docker stop redis-container || true
          # Remove existing Redis container if exists
          sudo docker rm redis-container || true
          # Run Redis container
          sudo docker run -d --name redis-container -p 6379:6379 redis
          # 컨테이너 생성 확인
          docker ps | grep redis-container
        EOF
```

- 먼저 git settings -> secrets and variables -> actions 에 .env파일에 저장해 두었던 비밀 키와 ssh_key, ec2_host를 저장한다. 그리고 franding 프로젝트를 배포하기 위한 단계를 구성하면 됩니다.
- Git clone -> docker install -> network 생성 -> franding 프로젝트 이미지를 생성할 Dockerfile -> 이미지 생성 -> 생성된 이미지로 컨테이너(network랑 연결된) 생성 -> nginx 설치 -> Dockerfile 생성 -> nginx.conf 파일 생성 -> 컨테이너 생성 후 서버 가동 -> redis 설치 후 서버 가동.

- 이 파일의 문제점은 만약 내가 docker 설치 후 franding 프로젝트의 Dockerfile만 만들고 싶을 때도 처음 단계부터 끝 단계까지 모두 실행합니다. 따라서 부분적인 통합이 불가능하고, 매번 처음부터 실행하기 때문에 소요시간이 많이 걸립니다.

- 장점은 aws ec2 서버를 열고 host랑 key 값만 설정해주면 배포까지 일사천리로 진행된다는 점입니다.

## 교육
### [멋사]
- **기간**: 2024년 3월 - 2024년 6월
- **교육 과목**: Python backend 과정