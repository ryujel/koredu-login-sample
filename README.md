# KorEdu 로그인 샘플 (Supabase + Vercel + GitHub 테스트용)

실제 KorEdu 앱과는 별개인, 배포 파이프라인만 확인해보는 아주 작은 샘플입니다.
파일 하나(`index.html`)로 되어 있고, 이메일/비밀번호 회원가입·로그인·로그아웃만 됩니다.

## 1. Supabase 프로젝트 만들기 (직접 하셔야 해요)
1. https://supabase.com 접속 → 로그인/가입 → "New project" 클릭
2. 프로젝트 이름/비밀번호(DB 비밀번호, 아무거나 기억할 값) 입력 → 생성 (1~2분 정도 걸려요)
3. 생성되면 왼쪽 메뉴 **Project Settings → API** 로 이동
4. **Project URL** 값과 **anon public** 키 값, 이 두 개를 복사해두세요

## 2. 이 프로젝트에 연결하기
`index.html` 파일을 열어서 아래 두 줄을 찾아 방금 복사한 값으로 바꿔주세요.

```js
const SUPABASE_URL = 'YOUR_SUPABASE_PROJECT_URL';
const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';
```

(anon key는 브라우저에 그대로 노출돼도 되는 공개용 키예요 — Supabase가 그렇게 설계했어요. DB 비밀번호나 `service_role` 키는 절대 여기 넣으면 안 돼요.)

## 3. (선택) 가입 즉시 로그인되게 하기
기본값은 회원가입하면 인증 이메일을 보내고, 그 메일을 확인해야 로그인이 돼요.
테스트를 더 빠르게 하고 싶으면: Supabase 대시보드 → **Authentication → Providers → Email** →
"Confirm email" 옵션을 꺼주세요. (테스트용 설정이니, 나중에 실제 서비스로 갈 땐 다시 켜는 걸 권장해요.)

## 4. GitHub에 올리기
터미널에서 이 폴더 기준으로:

```bash
git init
git add index.html README.md
git commit -m "KorEdu login sample"
git branch -M main
git remote add origin <새로 만든 GitHub 저장소 주소>
git push -u origin main
```

(GitHub에 새 저장소를 먼저 만들어두셔야 해요 — github.com에서 "New repository".)

## 5. Vercel에 배포하기
1. https://vercel.com 접속 → 로그인
2. "Add New... → Project"
3. 방금 올린 GitHub 저장소 선택 → Import
4. 설정 그대로 두고 "Deploy" (정적 HTML이라 빌드 설정 필요 없어요)
5. 배포 끝나면 나오는 주소(`https://...vercel.app`)로 접속해서 회원가입/로그인이 실제로 되는지 확인

## 확인이 끝나면
이 샘플은 테스트용이라 계속 써도 되고, 다 확인했으면 Vercel/GitHub에서 지워도 됩니다.
실제 KorEdu 앱을 옮길 때는 이 경험(회원 인증을 Supabase로 옮기는 방식)을 그대로 확장해서
`users.json`/`roster.json` 등 지금 로컬 파일로 저장 중인 데이터를 Supabase 테이블로 옮기게 됩니다.
