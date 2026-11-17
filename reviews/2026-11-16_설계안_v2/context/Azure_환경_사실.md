# Azure 환경 사실 자료 (2026-11-16 기준)

이 문서는 설계안 v2가 쓰겠다고 한 Azure 서비스를 실제로 어디에서, 어떤 권한으로 쓸 수 있는지 판단할 수 있도록 확인된 사실과 확인되지 않은 사실을 나눠 적은 것이다.

## 확인된 것: 팀이 받은 Azure 교육과 실습 환경

팀원들은 "GitHub Copilot + MS Azure 활용 AI 개발" 3일 과정(2026년 10~11월)을 들었다. 출처는 교육 교안(pptx)과 실습 노트북이다.

- 구독은 교육 운영 측이 관리한다. 교안 설명: "구독: 요금이 청구되는 단위. 학교가 관리".
- 실습 계정은 두 종류였다. 1일차는 개인 계정(41개), 2~3일차는 조 계정(10개 조)이다.
- 조 계정의 리소스 그룹 이름 형식은 `team_AIBIC2026_조번호_RG_EUS2`이고, 지역은 주로 East US 2다.
- 교안 규칙: "안내받은 리소스 그룹만 사용", "리소스 그룹은 새로 만들지 않음", "다른 사람 그룹은 건드리지 않기".
- 조 계정에는 Foundry 프로젝트가 미리 만들어져 있었다. 3일차에는 Foundry 리소스 키 하나로 채팅 모델, Vision, Speech, Translator, Language를 모두 호출했다.
- 교안 안내: 엔드포인트는 실습이 끝나면 삭제해 요금을 멈추고, 컴퓨팅 인스턴스는 쓰지 않을 때 중지한다.

실습에서 직접 만들거나 써 본 자원:

| 일차 | 자원 | 내용 |
|---|---|---|
| 1 | Azure ML 작업 영역, 컴퓨팅 인스턴스 | VS Code·GitHub Copilot 연결, 노트북 실행 |
| 1 | scikit-learn·PyTorch 모델을 MLflow 형식으로 저장 | 오염도·수분 두 숫자로 A·B·C 등급을 예측하는 수업용 가상 데이터. 정답은 "오염도 ≤10이고 수분 ≤5면 A, 오염도 ≤30이고 수분 ≤20이면 B, 나머지 C" 규칙과 일치한다 |
| 1 | Docker MySQL | 학습 데이터 300행을 넣고 읽어 학습 |
| 1 | Automated ML | 표 데이터 분류(VotingEnsemble), 이미지 분류(TrashNet 6종, 서버리스 H100, 검증 정확도 81.7%) |
| 1 | 모델 등록 + 관리형 온라인 엔드포인트 | Standard_D2a_v4 1대, REST 주소와 키로 Python에서 호출 |
| 2 | GPU 가상 머신 NV36ads_A10_v5 | Ollama(한국어 LLM, bge-m3 임베딩), ChromaDB, Neo4j 설치. Azure ML에서 SSH 터널로 접속 |
| 2 | LangChain | 프롬프트 템플릿, LCEL 체인, few-shot, PDF RAG, Multi-Query, HyDE, 대화형 RAG, Graph RAG |
| 3 | Microsoft Foundry | 모델 배포, 플레이그라운드, langchain-openai로 호출 |
| 3 | Foundry Tools | Vision(Image Analysis 4.0: 태그·물체·OCR), Speech(STT·TTS), Translator, Language(감정·핵심 구·개체명·PII 가리기) |
| 3 | 에이전트 | MCP 서버와 도구 호출, `langchain.agents.create_agent`, 총괄 에이전트 + 담당 에이전트 구조의 Streamlit 미니 프로젝트 "분리배출 도우미" |

## 확인된 것: 우리 코드가 이미 연결한 Azure 자원

- Foundry 배포 모델(gpt-4.1-mini)을 openai SDK로 호출한다(백엔드 `/c/questions`).
- Azure OpenAI chat/completions를 httpx로 호출한다(백엔드 `/api/v1/classify`의 제로샷 대체 경로).
- Microsoft Entra External ID로 로그인한다(프런트).
- 모델 가중치를 Azure Blob SAS URL에서 내려받는다(백엔드 `scripts/fetch_models.py`).
- Azure Maps Route Matrix를 호출하는 코드가 병합되지 않은 브랜치에 있다(`origin/feat/track-d-platform`).

## 확인되지 않은 것

- 대회 공지 원문. 저장소에 없다. 심사 기준, 제출물, 시연 형식, 마감 일정을 문서로 확인할 수 없다.
- 대회 기간에 쓸 Azure 구독, 예산, 크레딧 한도. 교육용 조 계정을 대회에도 계속 쓸 수 있는지 알 수 없다.
- 조 계정 리소스 그룹에서 설계안 v2가 요구하는 자원(Foundry Agent Service, Azure AI Search, Document Intelligence, Microsoft Fabric 용량, PostgreSQL Flexible Server, Container Apps, Application Insights, Content Safety)을 새로 만들 권한이 있는지.
- 서비스별 할당량: GPU, Azure OpenAI 분당 토큰(TPM), AI Search 계층.
- Microsoft Fabric 용량(F SKU)이나 체험판을 쓸 수 있는지.
