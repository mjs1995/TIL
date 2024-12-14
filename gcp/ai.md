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
