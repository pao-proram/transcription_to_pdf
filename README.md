📄 Teams Transcript → Meeting Notes PDF

This project converts raw Microsoft Teams transcripts into clean, structured meeting notes and exports them as a professional PDF document.

It uses OpenAI models for text cleaning and summarization, and reportlab for PDF generation.

🚀 Features
Cleans noisy transcripts (removes fillers like "yyy", "eee")
Improves grammar, punctuation, and readability
Keeps original meaning intact
Generates structured meeting notes in Polish
Creates a professional PDF with:
Sections and hierarchy
Bullet points
Action items table
Page numbering
Tracks token usage and estimated API cost
🧠 Processing Pipeline
Raw transcript input
Cleaning step (LLM)
Removes fillers
Fixes language issues
Structured note generation (LLM)
PDF rendering (ReportLab)
🏗️ Project Structure
.
├── main.ipynb          # Main notebook
├── pdf_generator.py    # PDF generation logic
├── README.md
└── requirements.txt
⚙️ Requirements

Install dependencies:

pip install openai reportlab
🔑 OpenAI Setup

Make sure you have your API key set:

export OPENAI_API_KEY="your_api_key_here"

or in Windows:

setx OPENAI_API_KEY "your_api_key_here"
🧾 Usage
1. Provide transcript
transcript = "your raw Teams transcript..."
2. Clean transcript
clean_response = client.responses.create(
    model="gpt-5-mini",
    instructions="""
    Clean Polish transcript:
    - remove fillers
    - fix typos
    - fix punctuation
    - do not shorten
    - preserve meaning
    """,
    input=transcript
)

clean_text = clean_response.output_text
3. Generate structured meeting note
response = client.responses.create(
    model="gpt-5-mini",
    instructions=PROMPT,
    input=clean_text
)

note = response.output_text
4. Export to PDF
save_meeting_note_to_pdf(note, "meeting_note.pdf")
🧩 Output Format

The generated note follows a strict structure:

EXECUTIVE SUMMARY (STRONA 0)

Informacje podstawowe
Data:
Typ:
Obszar:
Status:

Uczestnicy
- Name – role

Cel spotkania

Kluczowe ustalenia (TL;DR)

ZADANIA / ACTION ITEMS
A1 | task | owner | status

Otwarte tematy

NOTATKA SZCZEGÓŁOWA

1. Kontekst
2. Główne wątki
3. Decyzje
4. Kolejne kroki
💰 Cost Estimation

The notebook calculates approximate API cost:

cost = input_tokens * PRICE_INPUT + output_tokens * PRICE_OUTPUT

⚠️ Prices must be updated according to the official OpenAI pricing.
