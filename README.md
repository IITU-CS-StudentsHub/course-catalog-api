# Course Catalog API

A standalone backend project for a course catalog built with FastAPI and Pydantic.

## How to run

1. Create a virtual environment:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate  # macOS/Linux
   # or .venv\Scripts\Activate.ps1 on Windows
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Start the dev server:
   ```bash
   fastapi dev main.py
   ```
   The API will be available at http://127.0.0.1:8000. Interactive documentation is available at http://127.0.0.1:8000/docs.

## What was verified

The following requests were verified against the API:

| Request | Expected result |
| --- | --- |
| `/courses` | 6 courses; ai-integration first (32 likes), api-design last (11) |
| `/courses?is_elective=true` | 2 courses: ai-integration, api-design |
| `/courses?is_elective=false` | 4 courses: modern-frontend, web-security, backend-fastapi, databases-postgresql |
| `/courses?sort=title` | 6 courses alphabetically by title: ai-integration, api-design, backend-fastapi, modern-frontend, databases-postgresql, web-security |
| `/courses?page=1&page_size=2` | ai-integration, modern-frontend |
| `/courses?page=2&page_size=2` | web-security, backend-fastapi |
| `/courses?page=3&page_size=2` | databases-postgresql, api-design |
| `/courses?page=4&page_size=2` | an empty list `[]` |
| `/courses` (pagination defaults)| all 6 courses (page_size defaults to 20) |
| `/courses/web-security` | returns the "web-security" course |
| `/courses/nope` | returns a 404 code with the body `{"detail": "Course not found"}` |
| `/stats` (Bonus) | returns `{"total": 6, "total_credits": 28, "electives": 2}` |
| `/courses?q=react` (Bonus) | returns modern-frontend |
