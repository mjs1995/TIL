# Vertex AI
- ![image](https://github.com/user-attachments/assets/8b6c90d7-c7ee-41aa-b032-307783bfa30d)
- ```python
  import vertexai
  vertexai.init(project=PROJECT_ID, location=LOCATION)

  from vertexai.generative_models import GenerationConfig, GenerativeModel
  import time
  model = GenerativeModel("gemini-1.5-flash")

  import time

  def call_gemini(prompt, generation_config=GenerationConfig(temperature=1.0)):
      wait_time = 1
      while True:
          try:
              response = model.generate_content(prompt, generation_config=generation_config).text
              return response
              break  # Exit the loop if successful
          except Exception as e:  # Replace with the actual exception type
              time.sleep(wait_time)
              wait_time *= 2  # Double the wait time
  
  def send_message_gemini(model, prompt):    
      wait_time = 1
      while True:
          try:
              response = model.send_message(prompt).text
              return response
              break  # Exit the loop if successful
          except Exception as e:  # Replace with the actual exception type
              time.sleep(wait_time)
              wait_time *= 2  # Double the wait time

  prompt = "What do you think could be a good name for a flower shop that specializes in selling bouquets of dried flowers more than fresh flowers?"

  print(call_gemini(prompt))
  ```

# Gemini
- Google DeepMind가 개발한 강력한 생성 AI 모델 제품군으로, 텍스트, 코드, 이미지, 오디오, 비디오 등 다양한 형태의 콘텐츠를 이해하고 생성할 수 있습니다.
- Vertex AI의 Gemini API 
  - Vertex AI의 Gemini API는 Gemini 모델과 상호 작용하기 위한 통합 인터페이스를 제공합니다. 
  - 이를 통해 개발자는 이러한 강력한 AI 기능을 애플리케이션에 쉽게 통합할 수 있습니다. 
  - 최신 버전의 최신 세부 정보와 특정 기능은 공식 Gemini 설명서 를 참조하세요 .
- 제미니 모델
  - Gemini Pro : 다음을 포함한 복잡한 추론을 위해 설계되었습니다.
    - 대량의 정보를 분석하고 요약합니다.
    - 정교한 크로스 모달 추론(텍스트, 코드, 이미지 등)
    - 복잡한 코드베이스를 통한 효과적인 문제 해결.
  - Gemini Flash : 속도와 효율성을 위해 최적화되었으며 다음을 제공합니다.
    - 1초 미만의 응답 시간과 높은 처리량.
    - 다양한 작업에 대해 저렴한 비용으로 높은 품질을 제공합니다. 
    - 향상된 멀티모달 기능에는 공간 이해 개선, 새로운 출력 모드(텍스트, 오디오, 이미지), 기본 도구 사용(Google 검색, 코드 실행, 타사 기능) 등이 포함됩니다.

```python
from vertexai.generative_models import (
GenerationConfig,
GenerativeModel,
HarmBlockThreshold,
HarmCategory,
Image,
Part,
SafetySetting,
)
model = GenerativeModel("gemini-1.5-pro")

generation_config = GenerationConfig(
temperature=0.9,
top_p=1.0,
top_k=32,
candidate_count=1,
max_output_tokens=8192,
)

response = model.generate_content(
    "Why is the sky blue?",
    generation_config=generation_config,
)

print(response.text)
