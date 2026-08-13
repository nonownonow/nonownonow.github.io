---
title: "사람의 자리는 타자가 아니라 게이트다 — 우리가 갈아탄 개발 패러다임 7기둥"
description: "AI 에이전트 팀으로 일하기 시작하며 갈아탄 개발 방식 7가지 — 스펙 정본(SDD)·오케스트레이터 팀·완료조건=테스트·판단 원장·git 일원화·게이트 CI/CD·DORA — 를 비유 하나씩으로 설명하는 입문."
date: 2026-08-13
tags: [AI에이전트팀, SDD, TDD, 판단원장, CICD, DORA]
---

<div class="k-art">

<section class="k-hero">
<p class="k-marker">PARADIGM — 002</p>
<p class="k-hero__line">사람이 코드를 안 치는데,<br>코드가 늘어난다. <em>그럼 사람은 뭘 하나.</em></p>
<p class="k-hero__sub">지난 사흘, 국내 임상 CRO 고객사의 사내 챗봇을 0에서 다시 세우며 개발 방식 자체를 갈아탔다. 오늘 첫 제품 코드가 CI green 으로 랜딩했는데 사람이 타이핑한 줄은 없다 — 전부 AI 에이전트가 썼다. 그 답을 일곱 기둥으로, 비유 하나씩으로 설명한다.</p>
</section>

<section class="k-pillar">
<div class="k-pillar__no">01</div>
<div class="k-pillar__body">
<p class="k-pillar__meta">🏗️ 도면과 건물</p>
<h3>스펙이 정본이다 (SDD)</h3>
<p>건물(코드)에 문제가 생기면 벽을 덧대는 게 아니라 <strong>도면(스펙)을 고치고 건물을 다시 뽑는다.</strong> AI 가 재시공 비용을 거의 0으로 만들었기 때문에 성립하는 이야기다. 우리 도면에는 태스크 289건이 있고, 코드는 그 표현일 뿐이다. 첫날 한 일도 돌아가는 프로토타입을 버리고 스펙만 새 레포로 이관한 것이었다.</p>
</div>
</section>

<section class="k-pillar">
<div class="k-pillar__no">02</div>
<div class="k-pillar__body">
<p class="k-pillar__meta">📽️ 영화 촬영장</p>
<h3>팀은 오케스트레이터 하나와 전문 워커들</h3>
<p>감독(오케스트레이터)이 장면을 배정하고 촬영·조명·음향(구현·테스트·리뷰 워커)이 병렬로 일한다. 상위 모델 리드 + 경량 워커 조합이 단일 모델 대비 <a href="https://www.anthropic.com/engineering/built-multi-agent-research-system">+90.2%라는 Anthropic 실측</a>이 배치의 근거다. 사람의 자리는 카메라 앞이 아니라 모니터 뒤 — <strong>"오케이"와 "다시"를 외치는 자리</strong>다. 그 승인과 정정 한 건 한 건이 AI 팀의 훈련 데이터로 쌓인다.</p>
<figure class="k-fig k-fig--wide">
<svg viewBox="0 0 640 190" role="img" aria-label="사람 게이트에서 오케스트레이터를 거쳐 워커들로 흐르는 조직 다이어그램">
  <path class="k-d-acc" d="M60 95 L95 60 L130 95 L95 130 Z"/>
  <text class="k-d-label" x="95" y="99" text-anchor="middle">사람</text>
  <text class="k-d-text" x="95" y="152" text-anchor="middle">게이트 · 방향</text>
  <path class="k-d-mut" d="M228 62 C 190 34, 150 40, 128 62"/>
  <text class="k-d-text" x="178" y="34" text-anchor="middle">승인 · 정정 = 훈련 데이터</text>
  <path class="k-d-ink" d="M132 95 H 218"/><path class="k-d-ink" d="M210 89 L218 95 L210 101"/>
  <circle class="k-d-ink" cx="268" cy="95" r="40"/>
  <text class="k-d-label" x="268" y="91" text-anchor="middle">오케스트</text>
  <text class="k-d-label" x="268" y="106" text-anchor="middle">레이터</text>
  <path class="k-d-ink" d="M306 78 C 360 50, 400 42, 448 40"/><path class="k-d-ink" d="M440 34 L448 40 L440 46"/>
  <path class="k-d-ink" d="M310 95 H 448"/><path class="k-d-ink" d="M440 89 L448 95 L440 101"/>
  <path class="k-d-ink" d="M306 112 C 360 140, 400 148, 448 150"/><path class="k-d-ink" d="M440 144 L448 150 L440 156"/>
  <rect class="k-d-ink" x="456" y="22" width="120" height="36" rx="6"/>
  <text class="k-d-label" x="516" y="45" text-anchor="middle">구현 워커</text>
  <rect class="k-d-ink" x="456" y="77" width="120" height="36" rx="6"/>
  <text class="k-d-label" x="516" y="100" text-anchor="middle">테스트 워커</text>
  <rect class="k-d-ink" x="456" y="132" width="120" height="36" rx="6"/>
  <text class="k-d-label" x="516" y="155" text-anchor="middle">리뷰 워커</text>
</svg>
<figcaption>fig.1 — 타자를 놓는 대신 게이트와 방향을 잡는다</figcaption>
</figure>
</div>
</section>

<section class="k-pillar">
<div class="k-pillar__no">03</div>
<div class="k-pillar__body">
<p class="k-pillar__meta">🌡️ 고기 온도계</p>
<h3>"됐다"의 정의는 테스트다 (TDD)</h3>
<p>"익은 것 같다"는 문장이 아니라 <strong>심부온도 63도라는 측정</strong>이 완료의 정의다. 태스크 289건 전부 완료조건이 실행 가능한 테스트 명세로 적혀 있고, 구현보다 테스트가 먼저 온다. AI 는 지치지 않고 자신 있게 "됐습니다"라고 말하는 존재라서, 사람의 감 대신 기계 판정이 반드시 필요하다.</p>
</div>
</section>

<section class="k-pillar">
<div class="k-pillar__no">04</div>
<div class="k-pillar__body">
<p class="k-pillar__meta">📒 통장 거래내역</p>
<h3>신뢰는 판단 원장에 쌓인다</h3>
<p>신뢰는 선언이 아니라 <strong>기록의 잔고</strong>다. 모든 결정을 결정·왜·승인·수정 형식으로 남긴다 — 사흘간 55건, 실패와 정정 포함. 같은 유형에서 무수정 승인이 3회 연속이면 AI 의 권한이 한 칸 내려가고(사전 승인 → 선실행·후보고), 사람의 정정 1회면 즉시 원위치다. 실제로 사흘 사이 하향 1건이 발효됐고, 정정에 의한 리셋도 1건 일어났다.</p>
<p>백미는 AI 가 자기 판정을 뒤집은 사건 — 반대 입장을 가장 강하게 변호시키는 스틸맨 검증이, Anthropic 이 에이전트 16기·2주·2만 달러로 10만 라인 <a href="https://www.anthropic.com/engineering/building-c-compiler">C 컴파일러를 만든 실증</a>을 들고 왔고, 원장에는 "입장 수정"이 그대로 남았다.</p>
</div>
</section>

<p class="k-pull">지우면 홍보물이 되고, 남기면 훈련 데이터가 된다.</p>

<section class="k-pillar">
<div class="k-pillar__no">05</div>
<div class="k-pillar__body">
<p class="k-pillar__meta">📦 작업지시서와 운송장</p>
<h3>관리 도구는 git 하나</h3>
<p><strong>이슈는 도면에서 뽑아낸 작업지시서다.</strong> 단방향이라, 현장에서 지시서에 낙서를 해도 도면은 바뀌지 않는다 — 정본은 언제나 스펙이다. 진행 현황은 칸반 보드의 포스트잇이 아니라 태스크맵→이슈→PR 로 이어지는 체인으로 본다. 택배를 화이트보드가 아니라 운송장 번호로 추적하는 것과 같고, 이 체인은 그대로 인수인계 문서가 된다.</p>
<figure class="k-fig k-fig--wide">
<svg viewBox="0 0 640 124" role="img" aria-label="스펙에서 이슈, PR, main 으로 이어지는 단방향 체인 다이어그램">
  <rect class="k-d-acc" x="24" y="30" width="128" height="52" rx="6"/>
  <text class="k-d-label" x="88" y="52" text-anchor="middle">스펙 (정본)</text>
  <text class="k-d-text" x="88" y="70" text-anchor="middle">태스크맵 289</text>
  <path class="k-d-ink" d="M156 56 H 216"/><path class="k-d-ink" d="M208 50 L216 56 L208 62"/>
  <rect class="k-d-ink" x="222" y="30" width="110" height="52" rx="6"/>
  <text class="k-d-label" x="277" y="60" text-anchor="middle">이슈</text>
  <path class="k-d-ink" d="M336 56 H 396"/><path class="k-d-ink" d="M388 50 L396 56 L388 62"/>
  <rect class="k-d-ink" x="402" y="30" width="110" height="52" rx="6"/>
  <text class="k-d-label" x="457" y="60" text-anchor="middle">PR + 리뷰</text>
  <path class="k-d-ink" d="M516 56 H 576"/><path class="k-d-ink" d="M568 50 L576 56 L568 62"/>
  <text class="k-d-label" x="604" y="60" text-anchor="middle">main</text>
  <path class="k-d-mut" d="M277 88 C 240 108, 130 108, 92 88"/>
  <path class="k-d-mut" d="M100 94 L92 88 L101 84"/>
  <text class="k-d-text" x="186" y="114" text-anchor="middle">역방향 없음 — 낙서는 도면을 못 바꾼다 ✕</text>
</svg>
<figcaption>fig.2 — 단방향 파생: 스펙을 고치고, 지시서를 다시 뽑는다</figcaption>
</figure>
</div>
</section>

<section class="k-pillar">
<div class="k-pillar__no">06</div>
<div class="k-pillar__body">
<p class="k-pillar__meta">🛂 공항 검색대</p>
<h3>게이트 — red 면 못 들어온다</h3>
<p>삑 소리가 나면 지위 고하 없이 못 들어온다 — <strong>CI 가 red 인 코드는 main 진입 불가</strong>다. 그리고 검색대 자체도 시험한다. 오늘 프런트엔드 타입체크가 조용히 아무것도 검사하지 않은 채 통과하고 있는 것을, 일부러 오류를 심어 지나가 보는 방식으로 잡았다. 심은 오류에 초록불이 켜지면 탐지기가 꺼져 있다는 뜻이다. 게이트의 반대편 끝은 push=배포 — 이 블로그도 push 한 번으로 자동 배포된다. 사람이 지키는 것은 배포 버튼이 아니라 게이트의 규칙이다.</p>
</div>
</section>

<section class="k-pillar">
<div class="k-pillar__no">07</div>
<div class="k-pillar__body">
<p class="k-pillar__meta">🎛️ 자동차 계기판</p>
<h3>잘 가고 있는지는 DORA 로 잰다</h3>
<p>속도계만 보면 엔진 과열을 놓치고, 온도계만 보면 도로에 멈춰 선다. <a href="https://dora.dev">DORA</a> 는 속도(배포 빈도·변경 리드타임)와 안정(변경 실패율·복구 시간)을 <strong>동시에</strong> 재는 외부 기준이다. 우리는 아직 프로덕션 전이라 대체 정의(머지 빈도·PR 리드타임·게이트 red 율)로 잰다 — 못 재는 것을 잰다고 말하지 않는 것까지가 기준의 일부다.</p>
</div>
</section>

<div class="k-coda">
<p class="k-marker">공통점</p>
<p><strong>사람의 판단을 타이핑에서 빼내 게이트에 재배치한다.</strong> 스펙을 승인하고, 완료의 정의를 테스트로 못박고, 판단을 기록으로 남기고, red 앞에서 예외를 안 만드는 일. 코드를 치는 손은 AI 가 대신할 수 있지만 이 자리들은 대신하지 못한다.</p>
<p>AI 에이전트 개발을 시작한다면 도구 설치가 아니라 여기서 시작하기를 권한다 — <em>당신 프로젝트의 "됐다"는 지금 문장인가, 테스트인가?</em></p>
</div>

</div>
