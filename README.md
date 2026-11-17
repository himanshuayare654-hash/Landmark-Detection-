# Landmark Detection (VS Code Setup Guide)

Detects famous monuments/landmarks (Eiffel Tower, Taj Mahal, Statue of
Liberty, etc.) in a photo using Google Cloud Vision's Landmark Detection
feature.

## 1. Open the project in VS Code

Open the `landmark_detection` folder in VS Code (`File > Open Folder`).

## 2. Create a virtual environment (recommended)

In the VS Code terminal (`` Ctrl+` ``):

```bash
python -m venv venv
```

Activate it:

- Windows: `venv\Scripts\activate`
- macOS/Linux: `source venv/bin/activate`

Then select this interpreter in VS Code: `Ctrl+Shift+P` → "Python: Select
Interpreter" → choose the one inside `venv`.

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

## 4. Set up Google Cloud Vision API access

The Vision API needs credentials to run:

1. Go to https://console.cloud.google.com/ and create a project (or use
   an existing one).
2. Enable the **Cloud Vision API** for that project:
   `APIs & Services > Library > search "Cloud Vision API" > Enable`.
3. Create a **Service Account**:
   `IAM & Admin > Service Accounts > Create Service Account`.
4. Create a **JSON key** for that service account and download it
   (e.g. save it as `vision-key.json` inside the project folder).
5. Set the environment variable so the code can find it:

   **Windows (PowerShell)**
   ```powershell
   $env:GOOGLE_APPLICATION_CREDENTIALS = "vision-key.json"
   ```

   **macOS/Linux**
   ```bash
   export GOOGLE_APPLICATION_CREDENTIALS="vision-key.json"
   ```

   Tip: set this every time you open a new terminal, or add it to your
   shell profile / a `.env` file loaded by your setup.

Note: Google Cloud gives new accounts a free trial credit, and the Vision
API also has a free monthly usage tier, so light testing typically costs
nothing.

## 5. Run it

```bash
python main.py path/to/your/photo.jpg
```

or run `python main.py` with no arguments and it will prompt you for a
file path.

## Example output

```
Found 1 landmark(s):

1. Eiffel Tower  (confidence: 87.45%)
   Coordinates: 48.858372, 2.294481
   Map link:    https://www.google.com/maps?q=48.858372,2.294481
```

## Troubleshooting

- **"DefaultCredentialsError"** → `GOOGLE_APPLICATION_CREDENTIALS` isn't
  set correctly, or points to the wrong file path.
- **"PermissionDenied: 403"** → the Cloud Vision API isn't enabled on
  your project, or the service account lacks the "Cloud Vision API User"
  role.
- **"No landmarks detected"** → the API only recognizes well-known
  public landmarks; obscure buildings or generic scenery won't match.
- **Import error for `google.cloud.vision`** → make sure you installed
  requirements inside the *activated* virtual environment (check the
  interpreter selected in the bottom-right of VS Code).
