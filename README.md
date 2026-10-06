# BPPD H3 Prompt Director

아이디어와 이미지·영상·오디오 레퍼런스를 **MiniMax H3에 바로 넣을 수 있는 영상 프롬프트**로 정리하는 AI 스킬입니다. 카메라 움직임, 액션의 인과관계, 한국어 대사, 사운드와 장면 연속성을 하나의 영상 타임라인으로 구성합니다.

Codex용 스킬과 ChatGPT 커스텀 GPT용 지침·지식 파일을 함께 제공합니다.

## 주요 기능

- **입력에 맞는 모드 선택:** 텍스트 기반 T2VA, 첫 프레임 I2VA, 첫·마지막 프레임 FL2VA, 마지막 프레임 L2VA, 레퍼런스 기반 Ref2VA
- **멀티 레퍼런스 관리:** 캐릭터, 소품, 배경, 스타일, 움직임, 음성 레퍼런스의 역할과 번호 정리
- **멀티샷 연출:** 영상 길이에 맞춘 컷 구성과 타임스탬프, 구체적인 카메라 움직임
- **액션과 연속성:** 준비 → 행동 → 충돌 → 반응을 연결하고 캐릭터·의상·소품·공간 관계 유지
- **한국어 대사:** 입력한 대사의 원문, 화자 ID, 발화 방식과 타이밍 유지
- **사운드 구성:** 장면 속 소리와 배경 음악을 구분하고 행동에 맞춰 배치
- **클레이·스톱모션 연출:** 손으로 만든 표면, 점토 변형, 미니어처 조명 등 물성 표현

## 파일 구성

| 파일 | 용도 |
| --- | --- |
| [SKILL.md](skills/bppd-h3-prompt-director/SKILL.md) | Codex 등 스킬을 지원하는 에이전트용 지침 |
| [INSTRUCTIONS.txt](custom-gpt/INSTRUCTIONS.txt) | 커스텀 GPT의 지침 필드에 넣을 내용 |
| [H3_REFERENCE.md](custom-gpt/H3_REFERENCE.md) | 커스텀 GPT에 업로드할 상세 지식 파일 |
| [원본 문서](original/BPPD_H3_Prompt_Director_SKILL.md) | 제공된 원본을 수정 없이 보존한 파일 |

## Codex에서 사용하기

1. 이 저장소를 내려받습니다.
2. `skills/bppd-h3-prompt-director` 폴더를 사용자 스킬 폴더에 복사합니다. 기본 경로는 `~/.codex/skills/`이며, Windows에서는 `%USERPROFILE%\.codex\skills\`입니다.
3. 스킬이 인식되면 `$bppd-h3-prompt-director`와 함께 요청을 입력합니다.

```text
$bppd-h3-prompt-director
H3 R2V 15초 클레이 액션. 첨부한 이미지의 캐릭터와 차량을 유지하고,
추격 장면을 멀티샷으로 구성해줘. 대사는 “야! 빨리 타!” 그대로.
통합 프롬프트로 출력해줘.
```

## 커스텀 GPT에서 사용하기

1. 커스텀 GPT 편집 화면을 엽니다.
2. 지침 필드에 `custom-gpt/INSTRUCTIONS.txt`의 내용을 넣습니다.
3. 지식 파일로 `custom-gpt/H3_REFERENCE.md`를 업로드합니다.
4. 기존 GPT에 추가하는 경우 다른 지침과 충돌하지 않도록 통합합니다.

이 저장소는 적용할 파일을 제공합니다. GitHub에서 내려받는 것만으로 GPT에 자동 설치되지는 않습니다.

## 요청 예시

```text
H3 8초: 비 오는 골목에서 탐정이 뒤를 돌아보는 장면. 카메라는 천천히 접근.
```

```text
H3 첫프레임: 첨부한 이미지에서 시작해서 캐릭터가 문을 열고 나가게 해줘.
```

```text
H3 첫프레임 마지막프레임: 두 이미지 사이의 움직임을 자연스러운 연속 장면으로 연결해줘.
```

```text
H3 R2V 15초 클레이 멀티샷 액션. 한국어 대사를 유지하고 통합 프롬프트로 줘.
```

장면 설명은 기본적으로 영어로 작성하며, 사용자가 준 대사와 화면 속 문구는 원래 언어 그대로 유지합니다. 한국어 설명을 원하면 요청에 명시하세요.

## 출력 형태

텍스트·첫 프레임·마지막 프레임 기반 요청은 다음 항목으로 구성합니다.

```text
integrated_multimodal_description:
[Shot 1]
...
[Shot 2] At 00:04.200,
...

overall_soundscape:
...

non_diegetic_music:
...
```

Ref2VA 요청은 `subject_definitions`, `summary`, `retention_analysis`, `detailed_description`, `overall_soundscape`, `non_diegetic_music`으로 레퍼런스와 연출을 함께 정리합니다.

## 범위

이 스킬은 **영상 생성용 프롬프트를 작성**합니다. 영상 파일 생성, MiniMax 실행, API 연결 기능은 포함하지 않습니다.

원본의 MiniMax 공식 구조 관련 표현은 원본 작성자의 설명입니다. 이 패키지는 최신 MiniMax 사양과의 대조 검증을 포함하지 않으며, 실제 사용하는 서비스의 입력 형식과 지원 모드를 함께 확인하세요.