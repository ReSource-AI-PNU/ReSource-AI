# Re:Source AI

**정부가 한 해 10곳에만 해 주는 사업장 폐플라스틱 순환 진단을, AI 에이전트로 모든 중소 제조기업에**

부산·경남의 고무·플라스틱 제조 중소기업은 공장에서 나오는 폐플라스틱 흐름의 성질과 갈 곳을 모른 채 "가장 싼 소각"을 기본값으로 내보냅니다. Re:Source AI는 공장의 폐플라스틱을 흐름별로 진단해 공정 재투입·매각·단지 내 묶음 매각·열분해·소각 중 갈 곳을 정하고, 규정 검토와 비용·탄소 비교를 거쳐 이행 계획서, 지원사업 신청 초안, 견적 요청서까지 만듭니다. 문제 정의와 근거는 [문제 정의 v2](docs/문제정의_v2.md)에 있습니다.

## 저장소 구성

| 저장소 | 역할 |
|---|---|
| [ReSource-AI](https://github.com/ReSource-AI-PNU/ReSource-AI) (현재) | 설계 문서, 다이어그램, 발표 자료 |
| [backend](https://github.com/ReSource-AI-PNU/backend) | FastAPI 에이전트 API (Python) |
| [frontend](https://github.com/ReSource-AI-PNU/frontend) | Next.js 웹 앱 (TypeScript, Tailwind) |

## 문서

| 문서 | 설명 |
|---|---|
| [문제 정의 v2](docs/문제정의_v2.md) | 대상·순간·잃는 가치, 근거와 출처, 버린 근거, 서비스 흐름 v2, 시연 장면, 검증할 가정 |
| [설계안 v1](docs/ReSource_AI_설계안_v1.md) | 주제, 페인포인트, 데이터, 기술 스택, 아키텍처, 유저 플로우, 구현 범위, 리스크 |
| [아키텍처 다이어그램](docs/아키텍처_다이어그램.png) | 클라이언트 · API · 에이전트 6개 · 데이터 · 운영 계층 |
| [유저 플로우 시퀀스](docs/유저플로우_시퀀스.png) | 사진 업로드부터 견적 요청서 발송까지의 흐름 |

## 대회 6단계와 에이전트 매핑

| 단계 | 에이전트 역할 | 핵심 기술 |
|---|---|---|
| ① 식별·분류 | 사진·영상에서 품목, 재질, 이물질 탐지 | Azure ML (RT-DETR + ByteTrack), Document Intelligence, Azure OpenAI |
| ② 가능성 판단 | 오염도 등급과 형태별 단가로 재활용 가능성 판정 | Azure OpenAI, Fabric Lakehouse |
| ③ 규정 검토 | 순환자원 지정 품목 여부와 인정 요건 체크리스트 | Azure AI Search (조항 단위 RAG) |
| ④ 업종·기업 탐색 | 같은 산업단지 내 묶음 수거 후보와 처리업체 매칭 | PostgreSQL + PostGIS, OR-Tools |
| ⑤ 비용·탄소 비교 | 경로별 비용, 운송 포함 순 탄소, KAU 환산 | Azure Maps Route API, 배출계수 |
| ⑥ 최적안 제안 | 추천안 1개와 대안 2개, 견적 요청서·인계서 초안 | Azure OpenAI, Foundry 평가 |

## 기술 스택

- **에이전트**: Microsoft Foundry Agent Service + Microsoft Agent Framework
- **백엔드**: FastAPI (Python) on Azure Container Apps
- **프런트엔드**: Next.js + React
- **데이터**: Azure Database for PostgreSQL (PostGIS, pgvector), Microsoft Fabric, Azure Blob Storage
- **모델**: Azure Machine Learning + MLflow, RT-DETR, ByteTrack
- **운영**: Entra ID, Application Insights + OpenTelemetry, GitHub Actions, Bicep

## MVP 범위 (대회 시연)

- 입력: 사진과 30초 이내 영상, 성분표 PDF 선택
- 품목: 폐플라스틱과 포장재는 끝까지, 금속 스크랩과 폐목재는 식별과 규정 단계까지
- 지역: 부산 녹산국가산업단지 좌표에 가상 기업 30곳 배치
- 외부 발송: 모의 업체 메일함
