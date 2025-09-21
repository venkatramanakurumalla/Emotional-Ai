
# Empathica AI

Empathica AI is an advanced, emotionally intelligent chatbot designed to simulate human-like empathy and provide supportive, context-aware responses. It goes beyond simple sentiment analysis by incorporating a sophisticated model of emotions, hormones, mood, and reinforcement learning to adapt its responses over time.

## 🌟 Key Features

*   **Advanced Emotion Detection:** Analyzes user input for nuanced emotional states (e.g., joy, grief, anxiety, gratitude) using keyword matching and pattern recognition.
*   **Dynamic Emotional State:** Maintains an internal emotional state that evolves based on conversation history, featuring emotional inertia and transitions.
*   **Hormone Simulation System:** Simulates the effect of neurochemicals (like dopamine, serotonin, cortisol) on its "mood" and responses.
*   **Reinforcement Learning (RL):** Uses Q-learning to adapt its response strategy (e.g., validating, exploratory, solution-focused) based on the perceived effectiveness of past interactions.
*   **Crisis Intervention:** Detects phrases indicating suicidal ideation, self-harm, or abuse and responds with pre-defined, compassionate crisis messages and relevant helpline numbers (configurable by locale, e.g., IN for India).
*   **Relationship Bonding:** Tracks a "relationship bond" metric that strengthens with positive interactions.
*   **Mood Tracking:** Maintains a longer-term "mood" state based on recent emotional history.

## 🚀 Getting Started

1.  **Prerequisites:**
    *   Python 3.6 or higher.
    *   Required Python packages: `numpy`

    You can install numpy using pip:
    ```bash
    pip install numpy
    ```

2.  **Installation:**
    Simply download or clone the repository containing the like `emotion_ai.py`.

3.  **Running the Demo:**
    Execute the Python script to run the built-in test functions.
    ```bash
    python emotion_ai.py
    ```
    This will run a basic test and a comprehensive stress test, showcasing the AI's capabilities across a wide range of emotional inputs.

## 🧠 How It Works

1.  **Input Processing:** When a user sends a message, the `chat` method is called.
2.  **Emotion Inference:** The `infer_user_mental_state` method analyzes the text to detect emotions and their intensity, also flagging any crisis situations.
3.  **State & Action Selection:** The detected emotions are converted into a discrete "state" representation. The AI then uses its Q-table (via `choose_response_type`) to select the most appropriate response type (e.g., "validating" for sadness, "exploratory" for joy).
4.  **Response Generation:** The `generate_response` method selects a contextually appropriate message from a large template library based on the detected emotion and chosen response type.
5.  **Internal State Update:** The AI's internal emotional state, hormone levels, and mood are updated to reflect the conversation.
6.  **Learning:** After generating a response, the AI calculates a "reward" based on whether the user's emotional state improved. It then updates its Q-table to learn which response types are most effective in specific emotional states.
7.  **Crisis Handling:** If a crisis is detected, the AI bypasses the normal response generation and provides immediate, supportive crisis resources.

## 📂 File Structure & Persistence

*   The AI automatically saves its learned Q-table (its "memory" of what responses work best) to a file named `empathica_q_table.json` after every 10 chats and when the session ends.
*   On startup, it attempts to load this file to retain learned behavior from previous sessions.

## 🤖 Example Usage

```python
# Import is not directly possible from the current file structure,
# but you can instantiate the class directly from the script.

# Create an instance
empathica = EmpathicaAI(name="Dr. Lila", locale="IN", seed=42)

# Have a conversation
response1 = empathica.chat("I just got promoted at work! I'm so proud!")
print(response1)
# Output: "That's wonderful news! Your excitement really shines through. 😊 "

response2 = empathica.chat("But I'm also scared I won't be good enough.")
print(response2)
# Output: "It makes sense to feel afraid in that situation... 😰 "

# Get a system snapshot
state = empathica.snapshot()
print(f"My current mood is: {state['mood']}")
