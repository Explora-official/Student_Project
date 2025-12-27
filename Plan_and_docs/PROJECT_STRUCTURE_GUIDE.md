# Student CS Chatbot - Project Structure Guide

## 🏗️ Complete Folder Structure

Create this folder structure in VS Code:

```
student-cs-chatbot/
│
├── backend/                          # Node.js + Express + TypeScript backend
│   ├── src/
│   │   ├── config/                   # Configuration files (DB, LLM, env)
│   │   ├── models/                   # MongoDB schemas (User, Conversation, etc.)
│   │   ├── agents/                   # AI Agents (DSA, OS, Networks, etc.)
│   │   │   └── base/                 # Base agent interface/class
│   │   ├── workflows/                # LangGraph state machine
│   │   │   ├── nodes/               # Workflow nodes (classifier, router, etc.)
│   │   │   └── edges/               # Workflow edges (conditions)
│   │   ├── services/                 # Business logic services
│   │   │   ├── llm/                 # LLM provider abstraction
│   │   │   ├── session/             # Session management
│   │   │   ├── analytics/           # Analytics tracking
│   │   │   └── cache/               # Redis caching
│   │   ├── middleware/               # Express middleware (auth, rate-limit, etc.)
│   │   ├── routes/                   # API endpoints
│   │   ├── websocket/                # Socket.io handlers
│   │   ├── utils/                    # Helper functions
│   │   ├── types/                    # TypeScript type definitions
│   │   ├── app.ts                    # Express app configuration
│   │   └── server.ts                 # Server entry point
│   │
│   ├── tests/                        # Test files
│   ├── logs/                         # Log files (gitignored)
│   ├── .env.example                  # Environment variables template
│   ├── .env                          # Actual env vars (gitignored)
│   ├── .eslintrc.js                  # ESLint configuration
│   ├── .prettierrc                   # Prettier configuration
│   ├── tsconfig.json                 # TypeScript configuration
│   ├── package.json                  # Dependencies and scripts
│   └── README.md                     # Backend documentation
│
├── frontend/                         # React + TypeScript + Vite frontend
│   ├── src/
│   │   ├── components/               # React components
│   │   │   ├── common/              # Reusable UI components
│   │   │   ├── chat/                # Chat-specific components
│   │   │   ├── sidebar/             # Sidebar components
│   │   │   └── layout/              # Layout components
│   │   ├── pages/                    # Page components (routes)
│   │   ├── hooks/                    # Custom React hooks
│   │   ├── services/                 # API calls, WebSocket
│   │   ├── store/                    # State management (Zustand)
│   │   ├── utils/                    # Helper functions
│   │   ├── types/                    # TypeScript types
│   │   ├── styles/                   # Global CSS
│   │   ├── App.tsx                   # Root component
│   │   ├── main.tsx                  # Entry point
│   │   └── vite-env.d.ts            # Vite type definitions
│   │
│   ├── public/                       # Static assets
│   ├── .env.example                  # Frontend env template
│   ├── .env                          # Frontend env (gitignored)
│   ├── .eslintrc.js                  # ESLint config
│   ├── tailwind.config.js            # Tailwind CSS config
│   ├── tsconfig.json                 # TypeScript config
│   ├── vite.config.ts                # Vite configuration
│   ├── package.json                  # Dependencies
│   └── README.md                     # Frontend docs
│
├── docker-compose.yml                # Docker services (MongoDB, Redis)
├── .gitignore                        # Git ignore rules
└── README.md                         # Main project documentation
```

---

## 🎯 Build Order (What We'll Create Step-by-Step)

### Phase 1: Backend Foundation (Steps 1-8)
1. ✅ **Project structure** (this file)
2. **Backend package.json** - Dependencies and scripts
3. **TypeScript configuration** - Type safety setup
4. **Environment configuration** - Manage secrets and settings
5. **Database connection** - MongoDB setup
6. **Express server skeleton** - Basic API server
7. **Logging utility** - Track what's happening
8. **Error handling middleware** - Graceful error responses

### Phase 2: Database Models (Steps 9-12)
9. **User model** - Store user data
10. **Conversation model** - Store chat history
11. **Feedback model** - Collect user feedback
12. **Analytics model** - Track usage metrics

### Phase 3: Core Services (Steps 13-16)
13. **LLM service abstraction** - Talk to AI models
14. **Session manager** - Track user sessions
15. **Cache service** - Redis for performance
16. **Rate limiter** - Prevent abuse

### Phase 4: Agentic AI (Steps 17-24)
17. **Base Agent class** - Foundation for all agents
18. **Subject Classifier node** - Detect CS topic
19. **Intent Analyzer node** - Understand question type
20. **Router node** - Select right agent
21. **DSA Agent** - Data structures & algorithms expert
22. **OS Agent** - Operating systems expert
23. **Network Agent** - Networking expert
24. **LangGraph workflow** - Connect everything

### Phase 5: API Layer (Steps 25-28)
25. **WebSocket handlers** - Real-time messaging
26. **Conversation routes** - REST API for conversations
27. **Feedback routes** - Collect user input
28. **Analytics routes** - Dashboard data

### Phase 6: Frontend (Steps 29-40)
29. **Frontend setup** - Vite + React + TypeScript
30. **Tailwind + shadcn/ui** - Styling foundation
31. **API service** - HTTP client
32. **WebSocket hook** - Real-time connection
33. **Chat layout** - Main UI structure
34. **Message component** - Display messages
35. **MessageInput component** - User input
36. **Code block component** - Syntax highlighting
37. **Sidebar** - Conversation list
38. **Settings page** - User preferences
39. **State management** - Zustand setup
40. **Integration** - Connect frontend to backend

---

## 📊 How Components Work Together

```
User Types Message
       │
       ▼
Frontend (React)
       │
       ▼
WebSocket Connection
       │
       ▼
Backend API (Express)
       │
       ▼
LangGraph Workflow
       │
       ├── Classifier (What CS topic?)
       ├── Analyzer (What type of question?)
       └── Router (Which expert agent?)
       │
       ▼
Specialist Agent (e.g., DSA Agent)
       │
       ▼
LLM Service (Claude/GPT API)
       │
       ▼
Response Enhancement (Add code examples)
       │
       ▼
Stream Back to User
       │
       ▼
MongoDB (Save conversation)
```

---

## 🎓 Key Concepts Explained

### What is an "Agent"?
Think of agents as specialized tutors. Each one is an expert in a specific CS domain:
- **DSA Agent**: Knows algorithms, data structures, complexity analysis
- **OS Agent**: Understands processes, memory, file systems
- **Network Agent**: Expert in protocols, TCP/IP, routing

Each agent has:
- Custom system prompts (tells the LLM how to act)
- Domain-specific tools (e.g., code executor, visualizer)
- Specialized knowledge for their subject

### What is LangGraph?
LangGraph is like a "flowchart for AI decision-making". Instead of just asking one question to the LLM, we create a multi-step workflow:

1. **Classify** - "Is this about algorithms or networks?"
2. **Analyze** - "Do they want a definition or example?"
3. **Route** - "Send to the right specialist agent"
4. **Generate** - "Create the best response"
5. **Enhance** - "Add code examples if needed"

This makes responses more accurate and educational!

### Why Separate Frontend and Backend?
- **Frontend (React)**: Beautiful UI, fast interactions, runs in browser
- **Backend (Node.js)**: Secure API keys, talk to AI, manage database
- **WebSocket**: Real-time streaming (see AI "typing" live)

---

## 🚦 Next Step

We'll start with **Step 2: Backend package.json**

This file tells Node.js:
- What dependencies to install (Express, MongoDB, LangChain, etc.)
- What scripts to run (start server, run tests, etc.)
- Project metadata

**Ready to create the first file?** Let me know and I'll generate it with full explanations! 🚀
