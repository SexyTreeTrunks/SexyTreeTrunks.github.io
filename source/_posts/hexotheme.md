---
title: Hexo 테마적용 (Tranquilpeak theme)
date: 2018-09-26 18:18:42
tags:
	- hexo
	- hexotheme
	- hexoblog
category:
	- hexo
clearReading: true
thumbnailImage: https://i.pinimg.com/originals/a8/06/85/a806855b99f8cfaeee1ff2266eec3555.jpg
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
coverImage: /covers/cover1.jpg
coverMeta: in
comments: false
---

<!-- more -->
Tranquilpeak 테마 적용후 설정관련 정리

<!-- excerpt -->
{% alert warning %}
본 설정은 테마 설치&적용 후 해야하는 과정임
{% endalert %}

# 헥소 설정(`_config.yml`)
--------
### 포스트자원폴더 설정
커버이미지, 썸네일이미지, 걍 포스트에서 사용할 이미지 등등 포스트별로 이미지를 따로 관리하기 위해 포스트자원폴더를 설정하는거  

`post_asset_folder: true` 


### Relative link 설정
보통 기본적으로 false로 되어있으니 확인만 ㄱㄱ  
`relative_link: false` 

### Enable RSS feed
RSS피드설정을 하기위해선 먼저 관련 NPM모듈을 설치해줘야함  
1. 블로그루트폴더에서 `npm install hexo-generator-feed --save` 실행
2. 다음 내용 추가

{% codeblock lang:yml %}
feed:
    type: atom
    path: atom.xml
    limit: 20
{% endcodeblock %}

# Tranquilpeak 설정

### 언어 설정
테마가 한국어 지원이 안됨. tranquilpeak의 document에서 친절하게 설명되어있지만 블로그에 사용되는 stirng변수들을 일일히 한국어로 바꿔야하기때문에 매우 귀찮음  
따라서 걍 `블로그루트폴더/_config.yml`에서 `language: en`으로 설정 ㄱㄱ  

{% blockquote %}
참고로 언어파일(en.yml) 맨 끝에 `author`라는 변수가 있는데 거기서 about페이지에 보여지는 job 정보를 수정할수있음
{% endblockquote %}

### 검색기능 설정
tranquilpeak테마는 검색엔진으로 Algolia API를 사용  
회원가입 및 설정은 [여기](https://elfinlas.github.io/2018/06/07/hexo-usea-lgolia/)를 참고함

1. Alogolia에 회원가입ㄱㄱ (시간나면 튜토리얼도 함 해보셈)
2. 회원가입후 Alogolia의 dashboard에서 indices탭 클릭하고 새 인덱스 추가
3. 블로그 루트폴더에서 `npm install hexo-algolia --save` `npm install hexo-algoliasearch` 실행 ㄱㄱ 
4. 헥소디렉토리의 `_config.xml`에서 다음 추가(appid와 apikey는 Algolia dashboard에서 확인가능)
{% codeblock lang:yml %}
algolia:
  appId: "applicationId"
  apiKey: "saerch-only api key"
  adminApiKey: "admin api key"
  chunkSize: 5000
  indexName: "algolia에서 새로 추가한 인덱스 이름"
  fields:
    - content:strip:truncate,0,500
    - excerpt:strip
    - gallery
    - permalink
    - photos
    - slug
    - tags
    - title
{% endcodeblock %}

5. 환경변수 추가 `export HEXO_ALGOLIA_INDEXING_KEY=admin api key`
6. `hexo algolia` 수행하면 포스팅한 글들에 인덱싱이 새로 생성될거임(이것도 algolia dashboard에서 확인가능) 

### 기본페이지 설정
테마에서 제공하는 Archive, Tag, Category 페이지를 사용하기위한 설정  
간단하니까 [공식문서](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak/blob/master/DOCUMENTATION.md#enable-pages) 참조ㄱㄱ

# 테마수정하기
-----
### 테마배경화면, 프로필이미지 수정하기
테마에 사용되는 정적이미지들은 `themes/tranquilpeak/source/assets/images`에 저장됨  

**테마배경화면 수정:**
- 위의 경로에 원하는 배경화면 저장후 이름을 cover.jpg로 수정 ㄱㄱ

**프로필이미지 수정:**
- 위의 경로에 원하는 프로필이미지 저장(정사각형이미지가 좋음. 안그러면 좀 짜부됨)  
- `themes/tranquilpeak/_config.yml`열고 `author`항목에서 `picture: 저장한 이미지파일 이름`

{% blockquote %}
만약 나중에 테마의 scss파일을 수정할경우(ex-글꼴수정) `grunt build` 할때 테마의 `source/_images`경로에있는 파일들로 `source/assets/images` 의 파일이 생성되기때문에 배경이미지와 프로필이미지는 두 경로에 모두 저장해놓는게 좋음  
{% endblockquote %}

### 글꼴 수정하기
글꼴수정작업은 테마의 SCSS파일을 수정하는 작업이기때문에 수정후 별도의 모듈로 빌드해줘야 수정된부분이 테마에 반영됨  
1. `themes/tranquilpeak/`으로 이동하여 `npm install` 실행  
2. `bower install` 실행 (만약 실행안될경우 `npm install -save bower` 한뒤 다시 ㄱㄱ)
3. [여기](http://blog.lattecom.xyz/2016/05/08/tranquilpeak-theme-web-font/)참고해서 scss파일 수정ㄱㄱ
4. 파일수정 다했으면 `grunt build` ㄱㄱ
5. 블로그 루트폴더로 이동하고 `hexo server`실행하여 잘적용됬는지 확인 ㄱㄱ  


# 포스팅 관련 설정
-----
### front-matter 설정
포스팅할 md파일 상단에 게시물에 대한 기본설정을 해주는 부분을 {% hl_text yellow %}front-matter{% endhl_text %}라함  
tranquilpeak에서는 다양한 front-matter 설정변수를 제공함  

{% codeblock lang:yml %}
---
title: title
date: 2018-09-26 18:18:42
tags:
	- tag1
	- tag2
category:
	- category1
keywords: # 검색엔진에서 사용될 키워드 지정
- javascript
- hexo
clearReading: true # 게시물볼때 옆에 사이드바 치움
thumbnailImage: image-1.png # 썸네일이미지 지정(`source/_post/게시물md파일이름/`폴더 안에 해당 이미지가 있어야함)
thumbnailImagePosition: bottom # 썸네일이미지 위치지정
autoThumbnailImage: yes #thumbnailImage로 썸네일이미지가 지정안되어있을경우 cover이미지나 게시물의 이미지를 이용하여 자동으로 썸네일 지정 
metaAlignment: center # 게시물의 메타정보 정렬유형
coverImage: image-2.png  # 커버이미지 지정(이것역시 썸네일이미지처럼 게시물폴더안에 이미지가있어야함)
coverCaption: "A beautiful sunrise" # 커버캡션 지정(따로 지정해놓지않으면 게시물제목으로 설정됨)
coverMeta: out # 커버캡션을 cover이미지 안에 넣을건지 밖에 따로 놓을건지 설정
coverSize: full # 커버이미지 사이즈
gallery: # 
    - image-3.jpg "New York"
    - image-4.png "Paris"
    - http://i.imgur.com/o9r19kD.jpg "Dubai"
    - https://example.com/orignal.jpg https://example.com/thumbnail.jpg "Sidney"
comments: false #댓글기능
meta: false #메타정보
actions: false 
---
{% endcodeblock %}

### 포스트 excerpt 설정
excerpt설정을 하지않으면 인덱스페이지에 포스트의 전체글이 보여지게됨  
인덱스페이지에 포스트의 일부내용만 보여지게하고싶으면 `<!-- more -->`과 `<!-- excerpt -->`를 이용하여 인덱스페이지에 보여지는 부분과 안보여지는 부분을 설정해야함  
아래는 예시

{% codeblock %}
<!-- more -->
인덱스페이지에 보여질부분입니다.

<!-- excerpt -->
여기서부터 게시글 내용을 입력하시면 됩니다.
more태그와 excerpt태그는 함께 사용해야 적용됩니다
{% endcodeblock %}

