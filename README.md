# BPPD H3 Prompt Director

MiniMax H3 영상 프롬프트 제작용 개인 스킬입니다. 원본의 모드, 레퍼런스, 카메라, 액션, 한국어 대사, 사운드 및 연속성 규칙을 보존했습니다.

- `original/BPPD_H3_Prompt_Director_SKILL.md`: 제공된 원본
- `skills/bppd-h3-prompt-director/SKILL.md`: 이름과 설명 메타데이터를 추가한 스킬
- `custom-gpt/INSTRUCTIONS.txt`: 커스텀 GPT 지침 필드용
- `custom-gpt/H3_REFERENCE.md`: 커스텀 GPT 지식 파일용

## Codex

`skills/bppd-h3-prompt-director` 폴더를 사용자 스킬 디렉터리에 복사한 뒤 `$bppd-h3-prompt-director`로 호출하세요.

## 커스텀 GPT

GPT 편집 화면의 지침에 `custom-gpt/INSTRUCTIONS.txt`를 넣고, 지식에 `custom-gpt/H3_REFERENCE.md`를 업로드하세요. 기존 GPT의 다른 지침이 있으면 보존하며 통합하세요.

예시 요청: `H3 R2V 15초 클레이 액션, 한국어 대사 유지, 통합 프롬프트`

원본의 MiniMax 공식 구조 관련 표현은 원본 작성자의 설명이며, 이 패키지에서 최신 MiniMax 사양과 대조하여 검증한 것은 아닙니다.