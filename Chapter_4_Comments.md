# Chapter 4 : Comments

날짜: 2023년 5월 7일 → 2023년 5월 13일
요약: _"Comments Do Not Make UP for Bad Code"_. 주석을 다는 것은 코드 작성을 잘 하지 못한 `실패(failure)`를 보상하려는 심리에서 발생한다. 몇 가지 특수 목적 용도의 주석이 필요한 경우를 제외한 나머지 경우에서는 주석 작성보다 클린 코드에 보다 집중하자.

## Good Comments

- Legal Comments: 저작권 정보 및 소유권 표기 관련 문구 추가
- Informative Comments: 구현된 코드에 대한 기본 정보 추가 (하지만 가능하다면 함수명을 통해 보다 직관적으로 알아볼 수 있게 하고 주석을 줄이는 것이 이상적이다)
- Explanation of Intent: 작성된 코드와 관련하여 배경, 최종 결정에 영향을 미친 justifications들 추가
- Clarification: 애매한 인수의 뜻을 풀이하거나 return 값을 알아보기 쉽게 설명 추가 (하지만 이해를 돕고자 작성한 주석이 틀릴 수도 있는 걸 경계해야 한다)
- Warning of Consequences: 장시간 run-time 경고 등 타 개발자가 코드를 실행 전 주의할 사항 추가
- TODO Comments: 현재 상황으로 해결할 수 없는 한계로 future actions 추가
- Amplification
- Javadocs in Public APIs

## Bad Comments

- Mumbling
- Redundant Comments: 코드를 읽는 것보다 더 오래 걸리는 주석 지양
- Misleading Comments
- Journal Comments: 버전 컨트롤 시스템 사용으로 대체할 수 있는 소스 이력 관리 주석 지양
- Noise Comments, Scary Noise: 코드 작성 내용을 반복하며 그 이상 새로운 정보를 기재하지 않는 주석 지양 (대부분 코드 구조를 개선하여 주석을 대체할 수 있다)
- Don't Use a Comment When You Can Use a Function or a Variable
- Position Markers e.g., // Action ///////
- Closing Brace Comments
- Attributions and Bylines: 소스 버전 컨트롤 시스템에서 대체할 수 있는 주석 지양
- Commented-Out Code: 최종 버전이 아닌 코드를 남긴 주석 지양
- HTML Comments
- Nonlocal Information: 해당코드 위치에 맞지 않는 주석 지양
- Too much Information
- Function Headers
- Javadocs in Nonpublic Code

## Examples

- 데이터 사이언티스들의 Jupyter Notebook (Python) 활용 > [TensorFlow Google Colab 예제](https://www.tensorflow.org/tutorials/images/cnn)
- 특정 in/output 파일 타입을 읽고 쓰는 방법 설명 > [캐글 예제](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/discussion/402580)

```python
from Bio import SeqIO

# Open the FASTA file
filename = "/kaggle/input/cafa-5-protein-function-prediction/Train/train_sequences.fasta"
fasta_sequences = SeqIO.parse(open(filename),'fasta')

# Loop over each sequence and print its ID and length
for fasta in fasta_sequences:
    print(fasta)
    print("Sequence ID:", fasta.id)
    print("Sequence length:", len(fasta))
    break
```

- 튜토리얼 옵션을 주석 표시 > [캐글 예제](https://www.kaggle.com/code/mbnb8317/ds4c-tutorial-all-about-folium-pydeck?scriptVersionId=35512489)

```python
m = folium.Map([36, 128], zoom_start=7)

# you can try these options
# m = folium.Map([37, 128], zoom_start=7, tiles='Stamen Terrain')
# m = folium.Map([37, 128], zoom_start=7, tiles='Stamen Toner')

m
```
