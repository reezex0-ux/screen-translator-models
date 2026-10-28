# screen-translator-models

화면 번역기가 내려받는 모델 파일 중, 원래 공개된 곳에 없는 변환본을
올려 두는 저장소입니다. 파일은 [Releases](https://github.com/reezex0-ux/screen-translator-models/releases)에
있고, 이 저장소에는 코드가 없습니다.

Converted model files for Screen Translator that are not published anywhere
else. The files live in the Releases of this repository.

## quickmt-int8-v1

| 파일 | 크기(바이트) | SHA-256 |
| --- | --- | --- |
| `quickmt-en-ko-int8-model.bin` | 186,183,320 | `c6f5251589929fd6f1792bf12d50bde7f0bf5509e77b684b4d409fe9a627187f` |
| `quickmt-ja-en-int8-model.bin` | 208,401,549 | `ac5728ce3f48fcbca7666f00a711632d9d537bf8b1b17190c19b4e47bed0260c` |

### 출처 (Attribution)

- 영→한: [quickmt/quickmt-en-ko](https://huggingface.co/quickmt/quickmt-en-ko),
  리비전 `a32fa395ebc7b722a0c021e213ca5fec4065c5df`의 `model.bin`
- 일→영: [quickmt/quickmt-ja-en](https://huggingface.co/quickmt/quickmt-ja-en),
  리비전 `e9ae594ff322d95254d730867c6166b25fd2c704`의 `model.bin`
- 원 저작자: QuickMT ([quickmt](https://huggingface.co/quickmt))
- 라이선스: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
  이 변환본도 같은 CC BY 4.0을 따릅니다.

### 변경한 내용 (Changes)

원본 CTranslate2 `model.bin`의 Linear·임베딩 가중치를 INT8로 다시 썼습니다.
CTranslate2가 `compute_type="int8"`로 불러올 때 쓰는 것과 같은 규칙(출력 행마다
float32 배율 하나)을 썼고, 그 밖의 변수는 원래 형식(bfloat16·float16) 그대로입니다.
그래서 같은 장치에서는 원본을 INT8로 실행한 것과 같은 번역을 내지만, 원본을
FP16으로 실행한 결과와는 일부 문장이 다를 수 있습니다.

Linear and embedding weights of the original CTranslate2 `model.bin` were
re-encoded as INT8 with one float32 scale per output row, the same rule
CTranslate2 applies for `compute_type="int8"`. All other variables are unchanged.

토크나이저·어휘·설정 파일은 바꾸지 않았으므로 여기에 올리지 않습니다. 원래
저장소의 같은 리비전에서 받으면 됩니다. 변환 도구는 화면 번역기 저장소의
`tools/ct2_int8.py`입니다(비공개 저장소).
