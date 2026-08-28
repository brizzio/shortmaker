# ShortMaker

ShortMaker is a personal short-video generator based on MoneyPrinterTurbo. This
fork is currently focused on a simple workflow:

- generate scripts and keywords with OpenRouter
- fetch or use video materials
- generate voiceover with Azure TTS V1 / Edge TTS
- render subtitles and background music
- export the final MP4 from the local task folder

This README is intentionally minimal while the app is being customized.

## Requirements

- Python 3.11
- Git
- uv
- An OpenRouter API key for script and keyword generation
- A video source:
  - Pexels API key, or
  - your own local video files

Azure TTS V1 does not require an API key in this app.

## Run Locally

Clone your repo:

```powershell
git clone https://github.com/brizzio/shortmaker.git
cd shortmaker
```

Install Python 3.11 and dependencies:

```powershell
uv python install 3.11
uv sync --frozen
```

Start the WebUI:

```powershell
uv run streamlit run webui/Main.py --browser.gatherUsageStats=False
```

Open:

```text
http://localhost:8501
```

In the app:

1. Open `Ajustes`.
2. Select `OpenRouter` as the LLM provider.
3. Enter your OpenRouter API key.
4. Keep the default model `minimax/minimax-m3:free`, or choose another free
   model from https://openrouter.ai/models?variant=free.
5. Click the model connection test.
6. For voice, select `Azure TTS V1`.
7. For background music, use random music for the simplest setup.
8. For video source, use `Local file` or configure a Pexels API key.

Generated videos are saved under:

```text
storage/tasks/<task-id>/final-1.mp4
```

## Run On Google Colab

Open the Colab notebook:

[Open ShortMaker in Colab](https://colab.research.google.com/github/brizzio/shortmaker/blob/main/docs/ShortMaker.ipynb)

Recommended Colab settings:

1. Go to `Runtime > Change runtime type`.
2. Select `GPU`.
3. Run the notebook cells in order.
4. Enter your ngrok auth token when asked.
5. Open the public URL printed by the last cell.

Inside the WebUI, use the same basic setup:

- LLM provider: `OpenRouter`
- Model: `minimax/minimax-m3:free`
- Voice: `Azure TTS V1`
- Music: random background music
- Video source: Pexels or local files

## Useful Commands

Run focused tests:

```powershell
uv run pytest test/services/test_llm.py test/services/test_webui_llm_settings.py test/services/test_webui_i18n.py
```

Check git status:

```powershell
git status
```

## License

This project is derived from MoneyPrinterTurbo and keeps the original MIT
license. See [LICENSE](LICENSE).
