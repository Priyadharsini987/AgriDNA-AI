# AgriDNA AI

AgriDNA AI is a precision-agriculture project with a React-based interface for crop health monitoring and AI-assisted agricultural insights.

## Repository structure

- `agridna-ai-v3/agridna-v2/` — React 18 frontend application.
- `backend/` — backend application files and image assets.

## Frontend features

- User authentication, OTP verification, and onboarding screens
- Dashboard with crop and soil-health visualizations
- Leaf-image upload and AI scan workflow
- Crop memory and nutrient-tracking views
- Village map and outbreak-visualization interface
- Alerts, farm settings, and multilingual interface support

## Frontend setup

1. Open the frontend directory:

   ```bash
   cd agridna-ai-v3/agridna-v2
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Start the development server:

   ```bash
   npm start
   ```

The React development server normally opens at [http://localhost:3000](http://localhost:3000).

## Technology stack

- React 18
- Recharts
- JavaScript, HTML, and CSS

## Configuration and secrets

Some translation functionality uses an external API. Configure the required key through a local environment file or your deployment platform. Never commit real API keys, passwords, or production secrets. Keep local `.env` files out of Git.

## Notes

The frontend README inside `agridna-ai-v3/agridna-v2/` contains additional interface details. Backend setup instructions should be added alongside the backend's actual dependency and configuration files before deploying the backend independently.
