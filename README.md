# 🧭 CareerCompass: AI-Powered Career Roadmap & Resume Intelligence Platform

*A full-stack, AI-powered career roadmap generator, resume intelligence engine, and progress-tracking platform built on Flask and Google Gemini.*

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Flask](https://img.shields.io/badge/Flask-3.0+-green.svg)](https://flask.palletsprojects.com/)
[![Gemini](https://img.shields.io/badge/Google-Gemini-orange.svg)](https://ai.google.dev/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🧭 Overview

**CareerCompass** is an end-to-end AI career-development assistant that provides:

- **Personalized career roadmaps** with milestones, skills, and curated resources
- **Career chatbot** offering concise, actionable guidance
- **Resume analyzer** that extracts skills, strengths, weaknesses, and career options
- **Resume comparison engine** that contrasts your resume against a peer benchmark
- **Weekly progress tracker** with scoring, insights, and history
- **Browser-based multi-page frontend** powered by Flask templates

The system integrates tightly with **Google Gemini** for structured JSON outputs, robust error handling, and natural-language intelligence.

---

## 🏗️ System Architecture

### High-Level Architecture (CareerCompass Pipeline)
```
Browser (UI) ──► Flask Server ──► Gemini API
                        │
                        ▼
     Career Roadmaps / Resume Insights / Chat Guidance
                        │
                        ▼
                 JSON ↔ Dynamic Frontend
```

### Core Features of CareerCompass

| Feature               | Description                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| **Roadmap Generator** | Creates 3–5 tailored milestones based on skills, interests, and experience      |
| **Career Chatbot**    | Provides concise, actionable bullet-point advice                                |
| **Resume Analyzer**   | Extracts skills, strengths, weaknesses, career recommendations                  |
| **Progress Tracker**  | Weekly scoring, suggestions, and historical trend logging                       |
| **Resume Comparison** | Skill-level and experience-level comparison vs peer resumes                     |
| **Multi-page UI**     | Templates for home, chatbot, resume analyzer, roadmap, comparison, and tracking |

---

## ✨ Project Features in Detail

### 1. Career Roadmap Generator

**Endpoint:** `POST /generate-roadmap`

Outputs structured JSON with:

- ✅ Milestones with clear objectives
- ✅ Timeframes for each milestone
- ✅ Required skill lists
- ✅ Curated resource URLs
- ✅ Detailed descriptions

**Strict JSON validation** ensures frontend reliability.

**Example Request:**
```json
{
  "skills": "Python, Machine Learning",
  "interests": "AI Research",
  "experience_level": "Intermediate"
}
```

**Example Response:**
```json
{
  "roadmap": [
    {
      "milestone": "Master Deep Learning Fundamentals",
      "timeframe": "3 months",
      "skills": ["PyTorch", "Neural Networks", "CNNs"],
      "resources": ["https://pytorch.org/tutorials", "..."],
      "description": "Build strong foundation in deep learning..."
    }
  ]
}
```

---

### 2. CareerCompass Chatbot

**Endpoint:** `POST /chat`

- Responds with **plain text bullet points**
- Optimized for quick, actionable career advice
- Gemini prompt tuned for conciseness and clarity

**Example Request:**
```json
{
  "message": "How do I transition from software engineering to ML?"
}
```

**Example Response:**
```
- Start with online ML courses (Coursera, fast.ai)
- Build 2-3 ML projects for your portfolio
- Learn Python data science stack (NumPy, Pandas, scikit-learn)
- Contribute to open-source ML projects
- Network with ML engineers on LinkedIn
```

---

### 3. Resume Analyzer

**Endpoint:** `POST /analyze-resume`

**Extracts:**
- Skills inventory
- Strengths assessment
- Weaknesses identification
- Career path suitability (with fit scores)
- Resume improvement suggestions
- Experience level (Entry/Mid/Senior)

**Outputs fully validated JSON.**

**Example Request:**
```json
{
  "resume_text": "Software Engineer with 3 years experience in Python..."
}
```

**Example Response:**
```json
{
  "skills": ["Python", "Flask", "REST APIs"],
  "strengths": ["Strong backend development", "API design"],
  "weaknesses": ["Limited frontend experience"],
  "career_paths": [
    {
      "path": "Backend Engineer",
      "fit_score": 85,
      "reasoning": "Strong Python and API skills"
    }
  ],
  "experience_level": "Mid-level"
}
```

---

### 4. Progress Tracker

**Endpoint:** `POST /track-progress`

- Scores weekly career progress **(0–100)**
- Suggests next-week improvements
- Maintains full progress history in memory
- Auto-increments week number

**Ideal for incremental skill growth tracking.**

**Example Request:**
```json
{
  "activities": "Completed 2 ML courses, built a CNN project"
}
```

**Example Response:**
```json
{
  "week": 5,
  "score": 85,
  "feedback": "Excellent progress on ML fundamentals",
  "suggestions": [
    "Start working on a larger end-to-end project",
    "Practice deploying models to production"
  ],
  "history": [...]
}
```

---

### 5. Resume Comparison Engine

**Endpoint:** `POST /compare-resumes`

Compares user and peer resumes across:

- **Skill proficiency** (0–100 scores)
- **Experience level** + confidence scores
- **Actionable comparative insights**

**Example Request:**
```json
{
  "user_resume": "3 years Python, Flask...",
  "peer_resume": "5 years Python, Django, AWS..."
}
```

**Example Response:**
```json
{
  "skill_comparison": {
    "user_skills": ["Python: 75", "Flask: 80"],
    "peer_skills": ["Python: 90", "Django: 85", "AWS: 70"]
  },
  "experience_gap": "Peer has 2 more years of experience",
  "insights": [
    "Consider learning Django to match peer expertise",
    "Add cloud deployment skills (AWS/GCP)"
  ]
}
```

---

### 6. Multi-Page UI (Flask Templates)

CareerCompass includes user-facing pages:

| Route                 | Page                    |
|-----------------------|-------------------------|
| `/`                   | Home                    |
| `/roadmap`            | Roadmap Generator UI    |
| `/resume-analyzer`    | Resume Analyzer UI      |
| `/progress-tracker`   | Weekly Progress UI      |
| `/resume-comparison`  | Comparative Resume Tool |
| `/chatbot`            | Career Chatbot          |

---

## 💻 Installation & Setup

### Prerequisites
```bash
pip install flask flask-cors python-dotenv google-generativeai
```

### Quick Start

#### 1. Clone Repository
```bash
git clone <repo-url>
cd CareerCompass
```

#### 2. Set Up Environment Variables

Create a `.env` file in the root directory:
```env
GEMINI_API_KEY=your_api_key_here
```

CareerCompass loads this automatically using `python-dotenv`.

#### 3. Run the Application
```bash
python app.py
```

The server will start at: **http://127.0.0.1:5000/**

---

## 📁 Project Structure
```text
CareerCompass/
├── app.py                            # Main Flask application
├── templates/
│   ├── homepage.html                 # Landing page
│   ├── roadmap.html                  # Roadmap generator interface
│   ├── resume_analyzer.html          # Resume analysis interface
│   ├── progress_tracker.html         # Progress tracking interface
│   ├── resume_comparison.html        # Resume comparison interface
│   └── chatbot.html                  # Chatbot interface
│
├── static/                           # CSS, JS, assets
│   ├── css/
│   ├── js/
│   └── images/
│
├── .env                              # Environment variables (not committed)
├── requirements.txt                  # Python dependencies
└── README.md                         # This file
```

---

## 🔌 API Reference

### CareerCompass Endpoints

| Endpoint            | Method | Purpose                                              |
|---------------------|--------|------------------------------------------------------|
| `/generate-roadmap` | POST   | Build structured, multi-milestone career roadmap     |
| `/chat`             | POST   | Career chatbot for actionable bullet-point advice    |
| `/analyze-resume`   | POST   | Extracts skills, strengths, weaknesses, career paths |
| `/compare-resumes`  | POST   | User vs peer résumé comparison engine                |
| `/track-progress`   | POST   | Weekly score + improvement suggestions + history     |
| `/`                 | GET    | Home page                                            |
| `/roadmap`          | GET    | Roadmap generator page                               |
| `/resume-analyzer`  | GET    | Resume analyzer page                                 |
| `/progress-tracker` | GET    | Progress tracker page                                |
| `/resume-comparison`| GET    | Resume comparison page                               |
| `/chatbot`          | GET    | Chatbot page                                         |

---

## ✅ Strengths of CareerCompass

### Architecture
- ✅ Highly modular Flask application
- ✅ Strong JSON validation and fallback mocks
- ✅ Real-time Gemini integration for structured outputs

### Features
- ✅ Multi-view web interface suitable for deployment
- ✅ Covers a full career-development workflow
- ✅ Not just a single tool—comprehensive career suite

### Extensibility
- ✅ Clear extensibility for job-matching
- ✅ LLM scoring integration-ready
- ✅ Portfolio generation support

---

## ⚠️ Limitations

### Data Persistence
- Progress history stored in **memory** (non-persistent)
- No database backend (yet)
- User sessions not preserved across restarts

### API Reliability
- Gemini relies on prompt stability
- Malformed responses require regex fallback
- No retry mechanism for failed API calls

### Scalability
- Not optimized for enterprise-scale load
- No caching layer
- Single-threaded Flask (development mode)

---

## 🚀 Future Enhancements

### Backend Enhancements

- [ ] **MongoDB/PostgreSQL persistence** for user profiles
- [ ] **Authentication support** for personalized dashboards
- [ ] **Queue system** for large resume documents
- [ ] **Redis caching** for frequently accessed roadmaps
- [ ] **Rate limiting** for API endpoints
- [ ] **Async processing** for heavy computations

### AI Enhancements

- [ ] **Job-matching index** ranking using vector embeddings
- [ ] **Resume scoring** against real job descriptions
- [ ] **Personalized learning pathways** over time
- [ ] **Skill gap analysis** with industry benchmarks
- [ ] **Interview preparation** module
- [ ] **Salary prediction** based on skills and experience

### UI Enhancements

- [ ] **React/Next.js frontend** for smoother UX
- [ ] **Visual analytics** for progress history
- [ ] **Resume upload** + document parsing (PDF/DOCX)
- [ ] **Dark mode** toggle
- [ ] **Mobile-responsive design**
- [ ] **Interactive roadmap visualization**
- [ ] **Export reports** (PDF, CSV)

### Integration

- [ ] **LinkedIn integration** for profile import
- [ ] **GitHub integration** for project analysis
- [ ] **Job board APIs** (Indeed, LinkedIn Jobs)
- [ ] **Calendar integration** for milestone tracking
- [ ] **Email notifications** for progress updates

---

## 🔬 Use Cases

CareerCompass supports scenarios such as:

### For Job Seekers
- Creating personalized career roadmaps
- Analyzing resume strengths and weaknesses
- Comparing resumes with industry peers
- Tracking weekly skill development

### For Students
- Planning career transitions
- Identifying skill gaps
- Building learning roadmaps
- Tracking academic progress

### For Career Coaches
- Providing data-driven career advice
- Generating structured career plans
- Tracking client progress over time
- Benchmarking against industry standards

---

## 🧑‍💻 Author

**Aarush**  
AI/ML Engineer (CSE — AI & ML)  
Specializing in LLM systems, career intelligence models, and structured JSON generation at scale

Creator of **CareerCompass**, an AI-powered career navigation suite.

---

## 🙏 Acknowledgments

- Google Gemini API for AI capabilities
- Flask community for excellent web framework
- Open-source career development resources
- Beta testers and early users

---

## 📜 License

MIT Licence

---

## 🤝 Contributing

Contributions are welcome! Areas of interest:

- Adding new career analysis features
- Improving AI prompt engineering
- Building data persistence layer
- Creating visualization components
- Enhancing UI/UX design

Please feel free to submit a Pull Request or open an issue.

### Development Guidelines

- Follow PEP 8 for Python code
- Add docstrings to all functions
- Include unit tests for new endpoints
- Update documentation with changes
- Test JSON validation thoroughly

---

## 📞 Support

For questions or support:
- Open an issue on GitHub
- Contact: [aarushinc1@gmail.com]
- Check the [Wiki](link-to-wiki) for detailed API documentation

---

## 🔧 Troubleshooting

### Common Issues

**Issue:** Gemini API rate limit exceeded
- **Solution:** Implement request throttling, add retry logic

**Issue:** JSON parsing errors
- **Solution:** Check Gemini prompt formatting, validate response structure

**Issue:** Progress history lost on restart
- **Solution:** Implement database persistence (see Future Enhancements)

**Issue:** Slow response times
- **Solution:** Enable caching, optimize Gemini prompts

---

## 📚 Citation

If you use this work in your project, please cite:
```bibtex
@misc{careercompass2024,
  author = {Aarush},
  title = {CareerCompass: AI-Powered Career Roadmap & Resume Intelligence Platform},
  year = {2024},
  publisher = {GitHub},
  url = {https://github.com/yourusername/CareerCompass}
}
```

---

## 🌟 Demo

> **Note:** Add screenshots or a demo video here
```
[Demo GIF or screenshots would go here]
```

---

**Built with 🧭 to help people navigate their career journeys**
