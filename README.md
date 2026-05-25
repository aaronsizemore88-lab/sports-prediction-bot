# sports-prediction-bot
Sports Prediction Backend
A serverless backend that fans out sports prediction queries to multiple AI models via OpenRouter, keeping your API key secure on the server.
Deploy to Vercel (recommended, free tier works fine)

Push this folder to a GitHub repo
Go to vercel.com → New Project → import your repo
In project settings → Environment Variables, add:

OPENROUTER_API_KEY = your OpenRouter key (sk-or-...)
SITE_URL = your Vercel app URL (e.g. https://your-app.vercel.app)


Deploy — Vercel auto-detects the /api folder

Your endpoint will be: https://your-app.vercel.app/api/predict
How it works
POST /api/predict
Request body:
json{
  "query": "Who wins Chiefs vs Eagles on Sunday?",
  "models": [
    { "label": "GPT-4o", "id": "openai/gpt-4o" },
    { "label": "Claude Sonnet", "id": "anthropic/claude-sonnet-4-5" }
  ]
}
Response:
json{
  "results": [
    {
      "label": "GPT-4o",
      "id": "openai/gpt-4o",
      "result": {
        "pick": "Kansas City Chiefs",
        "confidence": 72,
        "reasoning": "Chiefs have home field advantage and Mahomes is healthy.",
        "key_factors": ["Home field", "Mahomes form", "Eagles secondary injuries"]
      },
      "error": null
    }
  ]
}
Find model IDs
Browse all available models at: https://openrouter.ai/models
Free models (append :free):

meta-llama/llama-3-70b-instruct:free
mistralai/mistral-7b-instruct:free
google/gemma-2-9b-it:free
