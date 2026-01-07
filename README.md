♾️ Infinity Recs
An Intelligent Cross-Domain Recommendation Engine

Infinity Recs is a sophisticated, multi-service recommendation system that delivers personalized suggestions across Books, Movies, Games, and Music. Unlike traditional, static recommenders, Infinity Recs leverages Reinforcement Learning (Proximal Policy Optimization – PPO) to continuously adapt to user behavior in real time.

By treating discovery as a learning problem, the system improves with every click, rating, and interaction—optimizing for long-term user satisfaction rather than one-off recommendations.

🚀 Vision

Most recommendation platforms operate in silos—your taste in books has no influence on your movie or game suggestions.

Infinity Recs aims to break those silos.

The long-term goal is a unified discovery engine where preferences in one domain (e.g., dark fantasy novels) can inform and enrich recommendations in others (e.g., RPG games or atmospheric films). User discovery is modeled as a sequential decision-making problem, where the AI learns to maximize “reward” through meaningful engagement.

🧠 Core Concept

Infinity Recs treats recommendation as a game:

State → Item features + user interaction history

Action → Recommended content

Reward → User feedback (ratings, likes, clicks, dislikes)

The system learns an optimal policy that balances exploration (discovering new content) and exploitation (refining known preferences).

🛠️ Tech Stack
Layer	Technology
Frontend	React, Vite, React Router, Clerk Authentication
Backend	Python (Flask), SQLAlchemy, Gunicorn / Waitress
AI / ML	PyTorch (PPO), Scikit-learn (k-NN, TF-IDF), Joblib
Database	PostgreSQL
External APIs	Spotify API, TMDB API

📂 Project Structure
INFINITY_RECS/
├── backend/                         # Backend microservices & ML models
│   ├── Datasets/                    # Raw datasets and processed data
│   ├── MODEL/                       # Trained RL models & artifacts
│   ├── cache/                       # Cached embeddings / intermediate results
│   ├── __pycache__/                 # Python bytecode cache
│   ├── .env                         # Backend environment variables
│   ├── .cache                       # Internal caching metadata
│   ├── .gitignore
│   ├── .gitkeep
│   │
│   ├── Songs.py                     # Music recommendation service (Spotify + PPO)
│   ├── Books.py                     # Book recommendation service
│   ├── Games.py                     # Game recommendation service
│   ├── Movies.py                    # Movie recommendation service (TMDB + Async)
│   │
│   ├── Movie_ppo.pt                 # Trained PPO model for movies
│   ├── game_ppo.pt                  # Trained PPO model for games
│   │
│   ├── README.md                    # Backend-specific documentation
│   └── eslint.config.js
│
├── frontend/                        # Frontend application (React + Vite)
│   ├── public/                      # Static public assets
│   ├── src/                         # React source code
│   ├── .env                         # Frontend environment variables
│   ├── .gitignore
│   ├── index.html
│   ├── package.json
│   ├── package-lock.json
│   ├── postcss.config.js
│   ├── tailwind.config.js
│   ├── vite.config.js
│   ├── eslint.config.js
│   └── README.md                    # Frontend-specific documentation
│
├── index.html                       # Root-level HTML entry (if applicable)
├── package.json                     # Root package configuration
├── package-lock.json
├── postcss.config.js
├── tailwind.config.js
├── vite.config.js
│
├── .gitattributes
└── README.md                        # Main project documentation

🧭 Architectural Overview

Backend (/backend)
Each content domain (Books, Movies, Games, Music) is implemented as an independent microservice, allowing:

Domain-specific models

Independent scaling

Clean separation of concerns

PPO models (*.pt) are stored separately to enable fast loading and experimentation.

Frontend (/frontend)
A modern React + Vite application that:

Provides a unified user dashboard

Communicates with backend services via APIs

Handles authentication, routing, and UI state

Model Artifacts (MODEL/, *.pt)
Stores trained reinforcement learning policies used for personalized recommendations.

Caching & Performance
The cache/ and .cache directories reduce recomputation overhead for embeddings and similarity lookups.

⚙️ How It Works: Hybrid Recommendation Engine

Infinity Recs uses a two-phase recommendation strategy to effectively handle the cold-start problem and long-term personalization.

Phase 1: Content-Based Filtering (Cold Start)

Uses TF-IDF vectorization and Cosine Similarity

Implements k-Nearest Neighbors (k-NN) to recommend items similar to:

Search queries

Initial user interactions

Ensures meaningful recommendations even with zero historical data

Phase 2: Reinforcement Learning (Personalization)

Activated after 5+ user interactions

Uses Proximal Policy Optimization (PPO)

Learns a policy that maps item features → optimal recommendations

Continuously updates based on real-time feedback

This hybrid approach ensures both immediate usability and long-term adaptability.

🧪 Reward Function Design

User feedback is translated into weighted reward signals:

Interaction	Reward
Rating	(rating / 5.0)
Like	+1.0
Watch / Complete	+0.75
Click	+0.5
Dislike	-1.0

Negative feedback is intentionally weighted strongly to prevent repeated poor recommendations.


📥 Installation & Setup
1. Prerequisites

Python 3.9+

Node.js & npm

PostgreSQL

2. Backend Setup

Clone the repository and install Python dependencies:

pip install flask flask_sqlalchemy flask_cors torch pandas numpy spotipy aiohttp scikit-learn


Update the SQLALCHEMY_DATABASE_URI in each backend service with your PostgreSQL credentials.

3. Frontend Setup
cd frontend
npm install
npm run dev

4. Running the Services

Each recommendation engine runs as an independent microservice:

Service	Command	Port
Music	python songs.py	5000
Books	python books.py	5001
Games	python games.py	5002
Movies	python movies.py	5003
🤝 Contributing & Roadmap

Infinity Recs is an evolving project. Planned enhancements include:

🔗 Centralized API Gateway to unify all services

🌐 Cross-domain preference mapping

🐳 Dockerized deployment

📊 Advanced user analytics & explainable recommendations

🧪 Offline RL evaluation and A/B testing framework

Contributions, feedback, and discussions are welcome.

📝 License

This project is licensed under the MIT License.
