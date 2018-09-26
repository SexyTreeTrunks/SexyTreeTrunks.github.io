---
title: Hexo 블로그 관련 정리
date: 2018-09-23 02:14:54
tags: 
- hexo
- github
- hexoblog
category: 
- hexo
clearReading: true
thumbnailImage: https://pbs.twimg.com/profile_images/476729162707644418/mQZOTo9f.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
coverMeta: in
comments: false
---

<!-- more -->
헥소로 깃허브블로그 구축할때 참고한 링크랑 필요한거 정리

<!-- excerpt -->
### 헥소 설치 및 시작
[헥소 시작](https://kdydesign.github.io/2017/06/23/start-hexo-blog/)    
[테마 설치](https://kdydesign.github.io/2017/07/07/hexo-themes/)  

### 게시물 작성하기
- `hexo new 게시물제목`  
일케하면 `블로그루트/source/_post` 경로안에 md파일 만들어짐.

### hexo layout 종류
* post
    - 파일경로 : `source/_posts`
    - 홈페이지에 게시되는 기본글. 
    - 디폴트 레이아웃임
 	- 명령어 : `hexo new 게시물제목` 혹은 `hexo new post 게시물제목`
* draft
	- 파일경로 : `source/_drafts`
    - 초안. 바로 게시하지 않고 작성할수 있음
    - 명령어: `hexo new draft 게시물제목`
    - 한번에 여러 포스트를 작성중일때, 바로 반영안할 포스트들을 모아놓는 저장공간

### 스캐폴드 만들기
포스트, 페이지, 드래프트를 만들떄 처음에 나오는 구조를 정의하는 파일  
scaffolds/ 안에있는 md파일을 수정하면됨  
자세한건 링크 참조


### 기본 명령어 모음
hexo 빌드(markdown -> html)  : `hexo generate` 또는 `hexo g`

로컬에서 확인: `hexo server`

github에 업로드: `hexo deploy` 혹은 `hexo d`

hexo 빌드 & github 업로드: `hexo g --d`


### 전역자원폴더(`/source/*`)와 포스트자원폴더
포스트에서 사용하는 자원(이미지,동영상,링크 등등)을 관리하는 폴더  
관리방법은 두가지가 있음  

+ 전역자원폴더 
     - 포스트에서 올린 모든 자원을 모두 한 폴더에서 관리
     - `/source` 안에 폴더만들면 해당 폴더명으로 접근할수있음.
     - 어느포스트에서나 동일하게 접근가능함.
+ 포스트자원폴더
     - 포스트마다 자원을 저장하는 폴더를 따로 생성&관리
          (새 글 만들때마다 자원폴더 생성됨)
     - `_config.yml` 에서 `post_asset_folder: true` 로 설정해야함
     - 주의사항 : `![](example.png)` 이렇게 사용하면 포스트상에서는 동작되지만, 카테고리, 태그, 어카이브 등으로 포스트를 접속할경우 url이 달라져서 이미지에 접근이 안됨. 따라서 이렇게 작성 `{% asset_img example.png 이미지제목 %}`


### 자동 태그 플러그인
[자동태그플러그인](http://futurecreator.github.io/2016/06/19/hexo-tag-plugins/)  
마크다운 같은 hexo 자체 문법이라고 생각하면됨. 쫌 쓸만함.

### 포스트삭제하기
[참고링크](http://futurecreator.github.io/2017/01/15/how-to-delete-post-in-hexo/)  
1. 해당 포스트의 md파일 삭제  
2. `hexo clean`  
3. `hexo g --d`  

### 브랜치관리(소스파일 관리)
[참고링크](https://nillk.github.io/2017/09/04/Hexo-source-managing-with-git-branch/)  
`hexo deploy`를 하게되면 깃허브에 렌더링된 정적파일들만 올라가기 때문에 소스파일을 관리하고싶다면 따로 올려야함. 소스파일과 정적파일들을 같은 repository에서 관리할경우 해당 폴더에서 새로 브랜치를파서 깃허브에 올리면됨. 자세한건 링크참조  

### 오픈그래프
[참고링크](http://futurecreator.github.io/2016/06/16/opengraph-social-meta-tag/)  
웹 사이트의 URL 링크 공유 시 미리보기를 만들 때 오픈그래프 태그를 사용  
`블로그루트/themes/landscape/_config.yml`에서 `Miscellaneous` 항목에서 설정가능  

