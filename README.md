# TMDB Movie Recommender

A Streamlit app that recommends 5 movies based on a user-provided title using TMDB data. It ranks candidates with TF‑IDF similarity (overview + genres) and a hybrid score combining similarity, rating, and popularity. Optional provider listing (Netflix, etc.) is included.

## Features
- Search a movie and get top 5 recommendations
- Filters: language, release year range, minimum rating
- Tunable hybrid scoring weights (similarity, rating, popularity)
- Provider availability by region (US/IN/GB/CA/AU)
- Fast caching for TMDB calls

## Requirements
- Python 3.11+
- TMDB API key set via environment (`TMDB_API_KEY`)

## Setup (Local)
1. Clone the repo and create a virtual env (optional).
2. Install dependencies:
	```powershell
	pip install -r requirements.txt
	```
3. Set your TMDB API key (v3 key or v4 token). Add to `.env`:
	```env
	TMDB_API_KEY="<your_tmdb_key_or_v4_token>"
	```
	or set in the shell:
	```powershell
	$env:TMDB_API_KEY = "<your_tmdb_key_or_v4_token>"
	```
4. Run the app:
	```powershell
	streamlit run "c:\Users\vivek gupta\Desktop\Movie Recommendation\streamlit_app.py"
	```

## Usage
- Enter a movie title (e.g., "Inception") and click Recommend.
- Adjust filters and weights in the sidebar.
- Optional: type a provider name (e.g., "Netflix") to filter availability.

## Heroku Deployment
1. Ensure `Procfile` exists with:
	```
	web: streamlit run streamlit_app.py --server.port=$PORT --server.address=0.0.0.0 --browser.serverAddress=0.0.0.0
	```
2. (Optional) Add `runtime.txt` to pin Python, e.g.:
	```
	python-3.11.9
	```
3. Commit and push to GitHub.
4. Create a Heroku app and set config vars:
	```powershell
	heroku create your-movie-recommender
	heroku config:set TMDB_API_KEY="<your_tmdb_key_or_v4_token>"
	```
5. Deploy:
	```powershell
	git push heroku main
	```

## Troubleshooting
- DNS errors (NameResolutionError / DNS refused): switch networks or set reliable DNS (1.1.1.1, 8.8.8.8), then:
  ```powershell
  ipconfig /flushdns
  netsh winsock reset
  ```
- Connection resets mid-render (10054): network/VPN/proxy issues. Reduce network calls (disable provider filter) or try another Wi‑Fi.
- TMDB auth:
  - v3 key: passed as query param
  - v4 token (JWT): sent as `Authorization: Bearer <token>`

## Project Structure
- `streamlit_app.py` — Streamlit UI
- `tmdb_recommender.py` — TMDB API helpers + ranking
- `requirements.txt` — Python dependencies
- `Procfile` — Heroku process definition
- `.env` — Local environment variables (DO NOT commit secrets)

## License
This repository includes a `LICENSE` file. Use according to its terms.

# Movie-Recommendation-Sentiment-Analysis