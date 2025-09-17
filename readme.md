MCQ Generator (Local Transformer Edition)

This project is a Streamlit-based application that generates multiple-choice questions (MCQs) from any uploaded PDF or text document using a local transformer model (Flan-T5). The application also evaluates the generated quiz for complexity and presents the results in a table format.

Features

Upload PDF or TXT files to extract text.

Generate customizable number of MCQs.

Specify subject and complexity level (tone).

Generates MCQs in structured JSON format.

Evaluates the quiz complexity (max 50 words) and provides a review.

Displays MCQs in a tabular format using Pandas.

Works locally with a transformer model, no OpenAI API needed.

Installation

Clone the repository:

git clone https://github.com/yourusername/mcq-generator.git
cd mcq-generator


Create a virtual environment and activate it:

python -m venv env
source env/bin/activate    # Linux/Mac
env\Scripts\activate       # Windows


Install dependencies:

pip install -r requirements.txt


Download the Flan-T5 model (or any transformer model) using Hugging Face:

pip install transformers

Usage

Run the Streamlit app:

streamlit run StreamLitAPP.py


Open the URL shown in your terminal (usually http://localhost:8501) in your browser.

Upload a PDF or TXT file containing the text for which you want to generate MCQs.

Set the following parameters in the form:

No. of MCQs: Number of questions to generate.

Subject: Name of the subject/topic.

Complexity level (Tone): Difficulty or tone, e.g., simple, medium, advanced.

Click Create MCQs.

The generated MCQs and the complexity review will appear:

MCQs are shown in a table.

Review is shown in a text area.

If the model does not generate valid JSON, the raw output is displayed.

Code Explanation
StreamLitAPP.py

Imports required libraries (Streamlit, Pandas, dotenv, local utils, and MCQ generator).

Loads the JSON template from response.json to define the MCQ structure.

Builds a Streamlit form to get user inputs (file, number of MCQs, subject, tone).

Reads uploaded file text using read_file().

Calls generate_evaluate_chain() to generate MCQs using a local transformer model.

Displays results:

Table format for MCQs (get_table_data()).

Text area for complexity review.

MCQGenerator.py

Uses a local Flan-T5 transformer model via Hugging Face transformers pipeline.

Defines prompts for:

Generating MCQs from text.

Reviewing MCQs for complexity and tone.

generate_evaluate_chain():

Accepts input dictionary: text, number of questions, subject, tone, response JSON template.

Returns a dictionary with:

"quiz" → generated MCQs (JSON or parsed from model output).

"review" → complexity analysis (max 50 words).

Utils

read_file(file):

Reads text from PDF or TXT files.

get_table_data(quiz_str):

Converts quiz JSON into a Pandas-friendly table for display.

JSON Template (response.json)
{
  "1": {
    "mcq": "<question1>",
    "options": {"A": "...", "B": "...", "C": "...", "D": "..."},
    "correct": "A"
  },
  "2": {
    "mcq": "<question2>",
    "options": {"A": "...", "B": "...", "C": "...", "D": "..."},
    "correct": "B"
  }
}


This template ensures that all generated MCQs follow a consistent format.

The model must return output following this structure.
