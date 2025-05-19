# Flask GitHub Pages Website

A simple Flask-based website that can be hosted on GitHub Pages.

## Setup

1. Clone this repository
2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Running Locally

To run the website locally:
```bash
python app.py
```
The website will be available at `http://localhost:5000`

## Deploying to GitHub Pages

1. Create a new repository on GitHub
2. Push your code to the repository
3. Go to repository Settings > Pages
4. Under "Source", select "GitHub Actions"
5. Create a new file `.github/workflows/flask.yml` with the following content:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Build
        run: |
          pip install gunicorn
          gunicorn app:app

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./
```

6. Commit and push the workflow file
7. Your site will be available at `https://<username>.github.io/<repository-name>`

## Project Structure

```
.
├── app.py              # Main Flask application
├── requirements.txt    # Python dependencies
├── static/            # Static files (CSS, images)
│   └── style.css
└── templates/         # HTML templates
    └── index.html
``` 