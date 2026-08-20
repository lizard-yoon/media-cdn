# media-cdn

인스타그램 Graph API 발행용 **공개 미디어 호스팅**.

## 왜 필요한가
Instagram 로그인 API(`graph.instagram.com`)는 **로컬 파일 업로드를 지원하지 않는다.**
2026-08-20 실측 — v21.0 / v22.0 / v23.0 전부 동일:

```
POST graph.instagram.com/v23.0/{ig-user-id}/media
     media_type=REELS & upload_type=resumable
→ 400 {"message":"The parameter video_url is required","code":100}
```

따라서 영상·이미지 모두 **공개 URL이 선행 조건**이다. 이 리포가 그 URL을 제공한다.
(대안이던 Facebook 경로는 페이지 연결이 필요하고 resumable 지원도 미검증이라 채택하지 않았다.)

## 사용법
1. 파일을 `ig/{계정}/` 아래에 넣고 push
2. raw URL을 매니페스트의 `media_url` 로 지정

```
https://raw.githubusercontent.com/lizard-yoon/media-cdn/main/ig/seoa/파일명.mp4
```

## 규칙
- **여기 올라가는 것은 인터넷 전체에 공개된다.** 어차피 SNS에 발행할 것만 넣는다.
- 개인정보·미공개 기획·자격증명은 **절대 금지**
- 파일명은 ASCII로(한글 파일명은 raw URL 인코딩이 번거롭다)
- 발행이 끝나 더 필요 없는 파일은 정리한다(용량 관리)
