# Weather Agent Demo

## 1. Objective
This notebook demonstrates how to build a simple agent using the `google-genai` library that can call a small function from LLM.  It's to query the internal table and return its corresponded value.

## 2. How to Use It

1.  **Install Libraries**: Ensure `google-genai` is installed by running the first code cell.
2.  **API Key Setup**: Set up your Gemini API key in Colab Secrets (named `GEMINI_API_KEY`) or enter it manually when prompted.
3.  **Run the Agent Logic**: Execute the cells containing the `WEATHER_DATA` definition, the `get_weather` function, and the `run_agent` function. These cells set up the agent's core logic and its available tool.
4.  **Interact with the Agent**: Use the `run_agent(prompt)` function to ask questions related to weather. The agent will determine if it needs to call the `get_weather` tool to answer your query. For example:
    ```python
    run_agent("What is the weather in the local database for 2025-12-17?")
    ```
    You can also ask general questions, and the agent will respond without invoking the tool.

## 3. Code Structure

*   **Installation (`!pip install google-genai`)**: Installs the necessary `google-genai` library.
*   **Local Data/Database Simulation (`WEATHER_DATA`)**: A dictionary simulating a small weather database.
*   **The Python Function (Tool - `get_weather`)**: A standard Python function that looks up weather data for a given date. This function is exposed to the generative model as a tool.
*   **The Core Agent Logic (`run_agent` function)**:
    *   **API Key Setup**: Configures the `google.generativeai` library with your API key.
    *   **Tool Registration**: The `get_weather` function is registered as a tool for the `generative_model`.
    *   **`run_agent(prompt)` function**: Orchestrates the interaction:
        1.  Sends the user's `prompt` to the `generative_model`.
        2.  Checks if the model requests a function call (e.g., `get_weather`).
        3.  If a function call is requested, it executes the corresponding Python function with the arguments provided by the model.
        4.  Sends the original prompt, the model's function call, and the function's output back to the model for a final, human-readable response.
*   **Test Cases**: Examples demonstrating how to use the `run_agent` function, showcasing both tool-use and direct responses from the LLM.
