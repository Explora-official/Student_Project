Student CS Chatbot System - Comprehensive Master Plan
Executive Summary
This document outlines the complete architecture, technology stack, and implementation strategy for a production-ready Student-Friendly Computer Science Chatbot system. The system leverages agentic AI workflows, modern full-stack technologies, and intelligent routing to provide educational CS support across multiple domains.

Table of Contents
System Architecture
Technology Stack
Database Design
Agentic Workflow Design
API Specifications
Frontend Architecture
Project Structure
Development Timeline
Security & Scalability
Future RAG Integration

1. System Architecture
1.1 High-Level Architecture
┌─────────────────────────────────────────────────────────────┐
│                         Client Layer                         │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐            │
│  │   React    │  │  WebSocket │  │    HTTP    │            │
│  │    SPA     │──│   Client   │──│   Client   │            │
│  └────────────┘  └────────────┘  └────────────┘            │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                      API Gateway Layer                       │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐            │
│  │   Express  │  │  Socket.io │  │    CORS    │            │
│  │   Router   │──│   Server   │──│ Middleware │            │
│  └────────────┘  └────────────┘  └────────────┘            │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    Application Layer                         │
│  ┌──────────────────────────────────────────────┐           │
│  │         LangGraph Agentic Orchestrator       │           │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐   │           │
│  │  │ Subject  │  │ Question │  │ Response │   │           │
│  │  │Classifier│→ │ Analyzer │→ │Generator │   │           │
│  │  └──────────┘  └──────────┘  └──────────┘   │           │
│  │         ↓           ↓            ↓           │           │
│  │  ┌──────────────────────────────────────┐   │           │
│  │  │      CS Domain Specialist Agents     │   │           │
│  │  │  • Data Structures & Algorithms      │   │           │
│  │  │  • Operating Systems                 │   │           │
│  │  │  • Computer Networks                 │   │           │
│  │  │  • Database Systems                  │   │           │
│  │  │  • Programming Languages             │   │           │
│  │  │  • Software Engineering              │   │           │
│  │  └──────────────────────────────────────┘   │           │
│  └──────────────────────────────────────────────┘           │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                      Service Layer                           │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐            │
│  │   LLM      │  │  Session   │  │  Analytics │            │
│  │  Service   │  │  Manager   │  │  Service   │            │
│  └────────────┘  └────────────┘  └────────────┘            │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                       Data Layer                             │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐            │
│  │  MongoDB   │  │   Redis    │  │  Vector DB │            │
│  │ (Primary)  │  │  (Cache)   │  │  (Future)  │            │
│  └────────────┘  └────────────┘  └────────────┘            │
└─────────────────────────────────────────────────────────────┘
1.2 Data Flow Diagram
User Query → WebSocket/HTTP → API Gateway → LangGraph Orchestrator
                                                      │
                                                      ▼
                                            Subject Classifier
                                                      │
                                                      ▼
                                            Specialist Agent Selection
                                                      │
                                                      ▼
                                            LLM Service (Claude/GPT)
                                                      │
                                                      ▼
                                            Response Enhancement
                                                      │
                                                      ▼
                                            Stream to Client ← MongoDB Store
1.3 Component Interaction
Client: React SPA with real-time streaming UI
API Gateway: Express.js with Socket.io for bidirectional communication
LangGraph Orchestrator: State machine managing conversation flow
Specialist Agents: Domain-specific prompt templates and tools
LLM Service: Abstraction layer for multiple LLM providers
Database: MongoDB for persistence, Redis for session caching

2. Technology Stack
2.1 Backend Stack
Technology
Version
Justification
Node.js
20.x LTS
Long-term support, excellent async performance
TypeScript
5.3+
Type safety, better developer experience, fewer runtime errors
Express.js
4.18+
Mature, well-documented, extensive middleware ecosystem
Socket.io
4.7+
Real-time bidirectional communication, fallback support
LangChain
0.1.x
Comprehensive LLM framework, active community
LangGraph
0.0.x
State machine for complex agentic workflows
MongoDB
6.0+
Flexible schema, excellent for conversation data
Mongoose
8.0+
ODM with TypeScript support, schema validation
Redis
7.2+
Session management, caching, rate limiting
ioredis
5.3+
TypeScript-friendly Redis client

2.2 Frontend Stack
Technology
Version
Justification
React
18.2+
Virtual DOM, component reusability, hooks for state management
TypeScript
5.3+
Type safety across full stack
Vite
5.0+
Fast HMR, optimized builds, modern tooling
TanStack Query
5.0+
Server state management, caching, optimistic updates
Zustand
4.5+
Lightweight global state (user preferences, UI state)
shadcn/ui
Latest
Accessible, customizable components built on Radix UI
Tailwind CSS
3.4+
Utility-first styling, consistent design system
React Markdown
9.0+
Render formatted responses with syntax highlighting
Prism.js
Latest
Code syntax highlighting for programming examples

2.3 AI/ML Stack
Technology
Version
Justification
Anthropic Claude
Latest
Superior reasoning, long context, safe responses
OpenAI GPT
gpt-4-turbo
Fallback option, strong general knowledge
LangSmith
Latest
LLM observability, debugging, performance tracking
Zod
3.22+
Schema validation for LLM outputs

2.4 Development & DevOps
Technology
Version
Justification
Docker
Latest
Containerization for consistent environments
Docker Compose
Latest
Multi-container orchestration
ESLint
8.x
Code quality and consistency
Prettier
3.x
Code formatting
Jest
29.x
Unit testing framework
Supertest
6.x
API integration testing
Playwright
Latest
E2E testing
Winston
3.x
Structured logging
Helmet
7.x
Security headers
Rate Limiter Flexible
3.x
API rate limiting


3. Database Design
3.1 MongoDB Collections
3.1.1 Users Collection
typescript
{
  _id: ObjectId,
  email: string,                    // Optional for anonymous users
  username: string,                 // Display name
  role: 'student' | 'admin',
  preferences: {
    explanationLevel: 'beginner' | 'intermediate' | 'advanced',
    codeExamplesEnabled: boolean,
    theme: 'light' | 'dark',
    language: string
  },
  metadata: {
    totalQuestions: number,
    favoriteSubjects: string[],
    lastActive: Date
  },
  createdAt: Date,
  updatedAt: Date
}
3.1.2 Conversations Collection
typescript
{
  _id: ObjectId,
  userId: ObjectId | null,          // null for anonymous
  sessionId: string,                // UUID for session tracking
  title: string,                    // Auto-generated from first question
  subject: string[],                // ['algorithms', 'data-structures']
  messages: [
    {
      role: 'user' | 'assistant' | 'system',
      content: string,
      timestamp: Date,
      metadata: {
        tokens: number,
        latency: number,
        agentUsed: string,
        confidence: number
      }
    }
  ],
  status: 'active' | 'archived',
  tags: string[],                   // For categorization
  feedback: {
    helpful: boolean | null,
    comments: string
  },
  createdAt: Date,
  updatedAt: Date
}
3.1.3 Feedback Collection
typescript
{
  _id: ObjectId,
  conversationId: ObjectId,
  messageIndex: number,
  userId: ObjectId | null,
  rating: number,                   // 1-5 scale
  feedbackType: 'helpful' | 'incorrect' | 'unclear' | 'incomplete',
  comment: string,
  context: {
    subject: string,
    questionType: string
  },
  createdAt: Date
}
3.1.4 Analytics Collection
typescript
{
  _id: ObjectId,
  date: Date,
  metrics: {
    totalQueries: number,
    averageResponseTime: number,
    subjectDistribution: {
      [subject: string]: number
    },
    errorRate: number,
    userSatisfaction: number
  },
  hourlyDistribution: number[],    // 24-element array
  createdAt: Date
}
3.2 Redis Cache Structure
Pattern: <prefix>:<key>

session:<sessionId>              → Session data (TTL: 24h)
rate_limit:<userId>:<endpoint>   → Rate limiting counters (TTL: 1h)
conversation:<conversationId>    → Active conversation cache (TTL: 1h)
llm_response:<hash>              → Cached LLM responses for common questions (TTL: 7d)
3.3 Indexes
javascript
// Users Collection
db.users.createIndex({ email: 1 }, { unique: true, sparse: true })
db.users.createIndex({ createdAt: -1 })

// Conversations Collection
db.conversations.createIndex({ userId: 1, createdAt: -1 })
db.conversations.createIndex({ sessionId: 1 }, { unique: true })
db.conversations.createIndex({ subject: 1 })
db.conversations.createIndex({ 'messages.timestamp': -1 })

// Feedback Collection
db.feedback.createIndex({ conversationId: 1 })
db.feedback.createIndex({ createdAt: -1 })

// Analytics Collection
db.analytics.createIndex({ date: -1 }, { unique: true })

4. Agentic Workflow Design
4.1 LangGraph State Machine
typescript
// State Definition
interface ConversationState {
  messages: BaseMessage[];
  currentSubject: string | null;
  detectedIntent: 'question' | 'clarification' | 'follow-up' | 'general';
  complexity: 'simple' | 'moderate' | 'complex';
  requiresCode: boolean;
  requiresVisualization: boolean;
  userContext: {
    level: 'beginner' | 'intermediate' | 'advanced';
    previousTopics: string[];
  };
  agentDecision: string;
  finalResponse: string;
  confidence: number;
}
4.2 Workflow Graph
START
  │
  ▼
┌─────────────────┐
│ Input Processor │  ← Sanitize, validate user input
└─────────────────┘
  │
  ▼
┌─────────────────┐
│Subject Classifier│  ← Identify CS domain(s)
└─────────────────┘
  │
  ├─ Data Structures/Algorithms
  ├─ Operating Systems
  ├─ Networks
  ├─ Databases
  ├─ Programming Languages
  └─ Software Engineering
  │
  ▼
┌─────────────────┐
│ Intent Analyzer │  ← Determine question type
└─────────────────┘
  │
  ├─ Definition/Concept
  ├─ How-To/Implementation
  ├─ Comparison
  ├─ Debugging/Error
  └─ Theory/Explanation
  │
  ▼
┌─────────────────┐
│Complexity Scorer│  ← Assess question difficulty
└─────────────────┘
  │
  ▼
┌─────────────────┐
│ Agent Selector  │  ← Route to specialist agent
└─────────────────┘
  │
  ▼
┌─────────────────────────────────┐
│   Specialist Agent Execution    │
│  ┌──────────────────────────┐   │
│  │  1. Retrieve Context     │   │
│  │  2. Construct Prompt     │   │
│  │  3. Call LLM             │   │
│  │  4. Validate Response    │   │
│  │  5. Enhance with Examples│   │
│  └──────────────────────────┘   │
└─────────────────────────────────┘
  │
  ▼
┌─────────────────┐
│Response Enhancer│  ← Add code blocks, diagrams
└─────────────────┘
  │
  ▼
┌─────────────────┐
│Quality Checker  │  ← Ensure educational value
└─────────────────┘
  │
  ├─ Pass → Stream to User
  └─ Fail → Regenerate or Fallback
  │
  ▼
END
4.3 Agent Definitions
Base Agent Interface
typescript
interface CSAgent {
  name: string;
  domain: string;
  systemPrompt: string;
  tools: Tool[];
  
  async process(state: ConversationState): Promise<{
    response: string;
    confidence: number;
    metadata: Record<string, any>;
  }>;
}
Specialist Agents
1. Data Structures & Algorithms Agent
Focus: Trees, graphs, sorting, searching, dynamic programming
Tools: Code executor, complexity analyzer, visualization generator
Prompt Template: Emphasis on time/space complexity, step-by-step walkthroughs
2. Operating Systems Agent
Focus: Processes, threads, memory management, file systems, scheduling
Tools: System diagram generator, process simulator
Prompt Template: Real-world examples, kernel-level explanations
3. Computer Networks Agent
Focus: OSI model, protocols, routing, TCP/UDP, security
Tools: Packet flow visualizer, protocol explainer
Prompt Template: Layer-by-layer breakdowns, practical scenarios
4. Database Systems Agent
Focus: SQL, normalization, transactions, indexing, NoSQL
Tools: Query optimizer, schema designer, ER diagram generator
Prompt Template: Hands-on SQL examples, performance considerations
5. Programming Languages Agent
Focus: Syntax, paradigms, best practices, language-specific features
Tools: Code formatter, debugger suggestions, pattern matcher
Prompt Template: Multi-language comparisons, idiomatic code
6. Software Engineering Agent
Focus: Design patterns, architecture, testing, CI/CD, agile
Tools: UML generator, code review suggestions
Prompt Template: Industry best practices, scalability focus
4.4 REact Pattern Implementation
For complex multi-step questions (e.g., "Design a URL shortener"):
Thought: User wants a system design. I need to break this into components.
Action: Identify requirements (functional, non-functional)
Observation: High availability, scalability needed

Thought: Need to explain database choice
Action: Compare SQL vs NoSQL for this use case
Observation: NoSQL better for key-value storage at scale

Thought: Security is important
Action: Explain hash collision handling
Observation: Base62 encoding + unique ID prevents collisions

Final Answer: [Comprehensive design with rationale]
4.5 Context Management Strategy
typescript
interface ContextWindow {
  recentMessages: Message[];        // Last 5 exchanges
  topicSummary: string;             // Auto-generated summary
  userPreferences: UserPreferences;
  relevantExamples: Example[];      // Retrieved from knowledge base
}

// Context Pruning Strategy
const buildContext = (state: ConversationState): string => {
  // 1. Always include current question (highest priority)
  // 2. Include immediately previous Q&A for follow-ups
  // 3. Include topic summary if conversation > 5 turns
  // 4. Prune old messages to stay within token limit (8k tokens)
  // 5. Add user level to adjust explanation depth
};

5. API Specifications
5.1 RESTful Endpoints
Authentication (Optional Phase 2)
POST   /api/auth/register         → Create account
POST   /api/auth/login            → Authenticate user
POST   /api/auth/logout           → End session
GET    /api/auth/me               → Get current user
Conversations
GET    /api/conversations         → List user conversations
POST   /api/conversations         → Create new conversation
GET    /api/conversations/:id     → Get conversation details
DELETE /api/conversations/:id     → Delete conversation
PATCH  /api/conversations/:id     → Update conversation (title, tags)
Messages
POST   /api/conversations/:id/messages    → Send message (alternative to WS)
GET    /api/conversations/:id/messages    → Get conversation history
Feedback
POST   /api/feedback              → Submit feedback
GET    /api/feedback/stats        → Get aggregate feedback
Analytics (Admin)
GET    /api/analytics/dashboard   → Get usage metrics
GET    /api/analytics/subjects    → Subject distribution
GET    /api/analytics/performance → Response times, error rates
5.2 WebSocket Events
Client → Server
typescript
// Join a conversation session
socket.emit('join', { 
  conversationId: string,
  userId?: string 
})

// Send a message
socket.emit('message', { 
  conversationId: string,
  content: string,
  context?: {
    level: string,
    includeCode: boolean
  }
})

// Request to stop generation
socket.emit('stop_generation', { 
  conversationId: string 
})

// Typing indicator
socket.emit('typing', { 
  conversationId: string,
  isTyping: boolean 
})
Server → Client
typescript
// Stream response chunks
socket.on('response_chunk', { 
  conversationId: string,
  chunk: string,
  isComplete: boolean 
})

// Message complete with metadata
socket.on('message_complete', { 
  conversationId: string,
  messageId: string,
  metadata: {
    tokens: number,
    latency: number,
    subject: string
  }
})

// Error handling
socket.on('error', { 
  code: string,
  message: string 
})

// Agent status updates
socket.on('agent_status', { 
  status: 'thinking' | 'retrieving' | 'generating',
  agent: string 
})
5.3 Request/Response Schemas
POST /api/conversations/:id/messages
Request:
json
{
  "content": "Explain binary search trees",
  "context": {
    "level": "beginner",
    "includeCode": true,
    "language": "python"
  }
}
Response:
json
{
  "messageId": "msg_123",
  "response": "A Binary Search Tree (BST)...",
  "metadata": {
    "subject": "data-structures",
    "agent": "DSA_Agent",
    "confidence": 0.95,
    "hasCode": true,
    "tokens": 450,
    "latency": 2300
  }
}
5.4 Error Response Format
json
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Too many requests. Please try again in 60 seconds.",
    "details": {
      "retryAfter": 60,
      "limit": 20,
      "window": "1m"
    }
  }
}
5.5 Rate Limiting
Anonymous Users:  10 requests/minute, 100 requests/hour
Registered Users: 30 requests/minute, 500 requests/hour
Premium Users:    100 requests/minute, 2000 requests/hour

6. Frontend Architecture
6.1 Component Tree
App
├── Providers
│   ├── ThemeProvider
│   ├── QueryClientProvider (TanStack Query)
│   └── AuthProvider
│
├── Layout
│   ├── Header
│   │   ├── Logo
│   │   ├── Navigation
│   │   └── UserMenu
│   │
│   ├── Sidebar (Desktop)
│   │   ├── ConversationList
│   │   ├── NewChatButton
│   │   └── Settings
│   │
│   └── Main
│       └── Router
│           ├── ChatPage
│           ├── HistoryPage
│           └── SettingsPage
│
└── ChatPage
    ├── ChatHeader
    │   ├── ConversationTitle
    │   └── SubjectBadges
    │
    ├── MessageList
    │   └── Message (repeat)
    │       ├── UserMessage
    │       │   ├── Avatar
    │       │   └── MessageContent
    │       │
    │       └── AssistantMessage
    │           ├── Avatar
    │           ├── MessageContent
    │           │   ├── MarkdownRenderer
    │           │   ├── CodeBlock
    │           │   └── MathRenderer
    │           │
    │           └── MessageActions
    │               ├── CopyButton
    │               ├── FeedbackButtons
    │               └── RegenerateButton
    │
    ├── TypingIndicator
    │
    └── MessageInput
        ├── TextArea
        ├── SendButton
        └── OptionsMenu
            ├── LevelSelector
            ├── CodeToggle
            └── LanguageSelector
6.2 Key Component Specifications
ChatPage.tsx
typescript
const ChatPage: React.FC = () => {
  const { conversationId } = useParams();
  const [messages, setMessages] = useState<Message[]>([]);
  const [isStreaming, setIsStreaming] = useState(false);
  const socket = useSocket();
  
  // Load conversation history
  const { data: conversation } = useQuery({
    queryKey: ['conversation', conversationId],
    queryFn: () => fetchConversation(conversationId)
  });
  
  // Handle incoming messages
  useEffect(() => {
    socket.on('response_chunk', handleChunk);
    socket.on('message_complete', handleComplete);
    return () => {
      socket.off('response_chunk');
      socket.off('message_complete');
    };
  }, [socket]);
  
  // Send message handler
  const sendMessage = (content: string, options: MessageOptions) => {
    socket.emit('message', {
      conversationId,
      content,
      context: options
    });
  };
  
  return (
    <div className="chat-container">
      <ChatHeader conversation={conversation} />
      <MessageList messages={messages} />
      {isStreaming && <TypingIndicator />}
      <MessageInput onSend={sendMessage} disabled={isStreaming} />
    </div>
  );
};
CodeBlock.tsx (with syntax highlighting)
typescript
interface CodeBlockProps {
  code: string;
  language: string;
  showLineNumbers?: boolean;
}

const CodeBlock: React.FC<CodeBlockProps> = ({ 
  code, 
  language, 
  showLineNumbers = true 
}) => {
  const [copied, setCopied] = useState(false);
  
  const copyCode = () => {
    navigator.clipboard.writeText(code);
    setCopied(true);
    setTimeout(() => setCopied(false), 2000);
  };
  
  return (
    <div className="code-block">
      <div className="code-header">
        <span className="language-tag">{language}</span>
        <button onClick={copyCode}>
          {copied ? <CheckIcon /> : <CopyIcon />}
        </button>
      </div>
      <SyntaxHighlighter
        language={language}
        style={vscDarkPlus}
        showLineNumbers={showLineNumbers}
      >
        {code}
      </SyntaxHighlighter>
    </div>
  );
};
6.3 State Management Strategy
Local Component State (useState):
UI interactions (modals, dropdowns)
Form inputs
Temporary UI state
TanStack Query (Server State):
Conversation history
User profile
Analytics data
Auto-refetch, caching, optimistic updates
Zustand (Global UI State):
typescript
interface AppStore {
  theme: 'light' | 'dark';
  sidebarOpen: boolean;
  userPreferences: UserPreferences;
  
  setTheme: (theme: 'light' | 'dark') => void;
  toggleSidebar: () => void;
  updatePreferences: (prefs: Partial<UserPreferences>) => void;
}
6.4 Styling Architecture
Tailwind Configuration:
javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: { /* Custom palette */ },
        code: { /* Syntax highlighting colors */ }
      },
      typography: { /* Prose styles for markdown */ }
    }
  },
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/forms')
  ]
}
Component Classes:
Use @apply for reusable component patterns
Maintain consistent spacing scale (4, 8, 12, 16, 24, 32, 48, 64)
Mobile-first responsive design
6.5 Performance Optimizations
Code Splitting:
Route-based splitting (React.lazy)
Component lazy loading for heavy features
Virtualization:
Virtual scrolling for long conversation lists (react-window)
Memoization:
React.memo for message components
useMemo for expensive computations
useCallback for event handlers
Streaming:
Progressive rendering of LLM responses
Chunked message display

7. Project Structure
7.1 Backend Structure
backend/
├── src/
│   ├── config/
│   │   ├── database.ts           # MongoDB & Redis config
│   │   ├── llm.ts                # LLM provider settings
│   │   └── environment.ts        # Environment variables
│   │
│   ├── models/
│   │   ├── User.ts
│   │   ├── Conversation.ts
│   │   ├── Feedback.ts
│   │   └── Analytics.ts
│   │
│   ├── agents/
│   │   ├── base/
│   │   │   ├── Agent.interface.ts
│   │   │   └── BaseAgent.ts
│   │   │
│   │   ├── DSAAgent.ts           # Data Structures & Algorithms
│   │   ├── OSAgent.ts            # Operating Systems
│   │   ├── NetworkAgent.ts       # Computer Networks
│   │   ├── DatabaseAgent.ts      # Database Systems
│   │   ├── PLAgent.ts            # Programming Languages
│   │   └── SEAgent.ts            # Software Engineering
│   │
│   ├── workflows/
│   │   ├── graph.ts              # LangGraph state machine
│   │   ├── nodes/
│   │   │   ├── classifier.ts
│   │   │   ├── analyzer.ts
│   │   │   ├── router.ts
│   │   │   └── enhancer.ts
│   │   └── edges/
│   │       └── conditions.ts
│   │
│   ├── services/
│   │   ├── llm/
│   │   │   ├── LLMService.ts
│   │   │   ├── ClaudeProvider.ts
│   │   │   └── OpenAIProvider.ts
│   │   │
│   │   ├── session/
│   │   │   └── SessionManager.ts
│   │   │
│   │   ├── analytics/
│   │   │   └── AnalyticsService.ts
│   │   │
│   │   └── cache/
│   │       └── CacheService.ts
│   │
│   ├── middleware/
│   │   ├── auth.ts
│   │   ├── rateLimiter.ts
│   │   ├── errorHandler.ts
│   │   ├── validator.ts
│   │   └── logger.ts
│   │
│   ├── routes/
│   │   ├── auth.routes.ts
│   │   ├── conversation.routes.ts
│   │   ├── feedback.routes.ts
│   │   └── analytics.routes.ts
│   │
│   ├── websocket/
│   │   ├── handlers/
│   │   │   ├── message.handler.ts
│   │   │   └── connection.handler.ts
│   │   └── socket.ts
│   │
│   ├── utils/
│   │   ├── logger.ts
│   │   ├── validators.ts
│   │   └── helpers.ts
│   │
│   ├── types/
│   │   ├── conversation.types.ts
│   │   ├── agent.types.ts
│   │   └── api.types.ts
│   │
│   ├── app.ts                    # Express app setup
│   └── server.ts                 # Server entry point
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── .env.example
├── .eslintrc.js
├── .prettierrc
├── tsconfig.json
├── package.json
└── README.md
7.2 Frontend Structure
frontend/
├── src/
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button/
│   │   │   ├── Input/
│   │   │   ├── Modal/
│   │   │   └── Spinner/
│   │   │
│   │   ├── chat/
│   │   │   ├── ChatHeader/
│   │   │   ├── MessageList/
│   │   │   ├── Message/
│   │   │   │   ├── UserMessage.tsx
│   │   │   │   ├── AssistantMessage.tsx
│   │   │   │   └── SystemMessage.tsx
│   │   │   ├── MessageInput/
│   │   │   ├── CodeBlock/
│   │   │   └── TypingIndicator/
│   │   │
│   │   ├── sidebar/
│   │   │   ├── Sidebar/
│   │   │   ├── ConversationList/
│   │   │   └── NewChatButton/
│   │   │
│   │   └── layout/
│   │       ├── Header/
│   │       ├── Layout/
│   │       └── MobileNav/
│   │
│   ├── pages/
│   │   ├── ChatPage.tsx
│   │   ├── HistoryPage.tsx
│   │   ├── SettingsPage.tsx
│   │   └── HomePage.tsx
│   │
│   ├── hooks/
│   │   ├── useSocket.ts
│   │   ├── useConversation.ts
│   │   ├── useMessages.ts
│   │   └── usePreferences.ts
│   │
│   ├── services/
│   │   ├── api.ts
│   │   └── websocket.ts
│   │
│   ├── store/
│   │   ├── appStore.ts           # Zustand store
│   │   └── queryClient.ts        # TanStack Query config
│   │
│   ├── utils/
│   │   ├── formatters.ts
│   │   ├── validators.ts
│   │   └── constants.ts
│   │
│   ├── types/
│   │   ├── message.types.ts
│   │   ├── conversation.types.ts
│   │   └── api.types.ts
│   │
│   ├── styles/
│   │   ├── globals.css
│   │   └── themes.css
│   │
│   ├── App.tsx
│   ├── main.tsx
│   └── vite-env.d.ts
│
├── public/
│   ├── favicon.ico
│   └── robots.txt
│
├── .env.example
├── .eslintrc.js
├── tailwind.config.js
├── tsconfig.json
├── vite.config.ts
├── package.json
└── README.md
7.3 Shared Types Package (Optional)
shared/
├── src/
│   ├── types/
│   │   ├── api.types.ts
│   │   ├── conversation.types.ts
│   │   └── user.types.ts
│   │
│   └── index.ts
│
├── tsconfig.json
└── package.json

8. Development Timeline
Phase 1: Foundation (Weeks 1-2)
Week 1: Setup & Core Architecture
Initialize monorepo structure
Setup TypeScript configs
Configure MongoDB and Redis
Setup Docker Compose for local development
Implement basic Express server
Setup authentication middleware
Create database models
Setup logging and error handling
Week 2: Frontend Foundation
Initialize Vite + React + TypeScript
Setup Tailwind CSS and shadcn/ui
Implement basic layout components
Setup routing
Configure TanStack Query
Create basic UI components library
Implement theme system
Phase 2: Core Chat Functionality (Weeks 3-4)
Week 3: Backend Chat System
Implement WebSocket server
Create message handling logic
Setup LLM service abstraction
Integrate Claude API
Implement conversation persistence
Add session management
Create rate limiting
Week 4: Frontend Chat Interface
Build chat UI components
Implement WebSocket client
Add message streaming
Create markdown renderer
Implement code syntax highlighting
Add conversation history
Build message input with options
Phase 3: Agentic Workflow (Weeks 5-6)
Week 5: LangGraph Implementation
Design state machine graph
Implement classifier node
Create intent analyzer
Build router logic
Implement response enhancer
Add context management
Create agent base class
Week 6: Specialist Agents
Implement DSA Agent
Implement OS Agent
Implement Networks Agent
Implement Database Agent
Implement Programming Languages Agent
Implement Software Engineering Agent
Test agent routing and responses
Phase 4: Enhancement & Polish (Weeks 7-8)
Week 7: Advanced Features
Implement feedback system
Add analytics tracking
Create admin dashboard
Implement conversation search
Add export functionality
Optimize performance
Add error recovery
Week 8: Testing & Documentation
Write unit tests (80%+ coverage)
Write integration tests
Perform E2E testing
Load testing and optimization
Write API documentation
Create user guide
Write deployment guide
Phase 5: Production Readiness (Week 9)
Security audit
Performance optimization
Setup monitoring (Sentry, LogRocket)
Configure CI/CD pipeline
Setup staging environment
Final bug fixes
Production deployment
Post-launch monitoring
Phase 6: RAG Integration (Future - Weeks 10-12)
Setup vector database (Pinecone/Chroma)
Implement PDF ingestion pipeline
Create embedding generation
Build semantic search
Integrate RAG into agent workflow
Test with CS textbooks/papers
Fine-tune retrieval parameters

9. Security & Scalability
9.1 Security Measures
Input Validation:
typescript
// Sanitize user input
import DOMPurify from 'isomorphic-dompurify';
import { z } from 'zod';

const MessageSchema = z.object({
  content: z.string()
    .min(1)
    .max(4000)
    .transform(val => DOMPurify.sanitize(val)),
  conversationId: z.string().uuid()
});
Rate Limiting:
typescript
import { RateLimiterRedis } from 'rate-limiter-flexible';

const rateLimiter = new RateLimiterRedis({
  storeClient: redisClient,
  keyPrefix: 'rl',
  points: 30,           // Number of requests
  duration: 60,         // Per 60 seconds
  blockDuration: 60     // Block for 60s if exceeded
});
Authentication (JWT):
typescript
interface JWTPayload {
  userId: string;
  role: string;
  iat: number;
  exp: number;
}

// Token expires in 7 days
const token = jwt.sign(
  { userId, role },
  process.env.JWT_SECRET,
  { expiresIn: '7d' }
);
HTTP Security Headers (Helmet):
typescript
app.use(helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      scriptSrc: ["'self'"],
      imgSrc: ["'self'", "data:", "https:"]
    }
  },
  hsts: {
    maxAge: 31536000,
    includeSubDomains: true,
    preload: true
  }
}));
API Key Security:
typescript
// Store in environment variables, never in code
const llmConfig = {
  anthropic: {
    apiKey: process.env.ANTHROPIC_API_KEY!,
    model: 'claude-3-5-sonnet-20241022'
  },
  openai: {
    apiKey: process.env.OPENAI_API_KEY!,
    model: 'gpt-4-turbo-preview'
  }
};

// Rotate keys regularly via secret manager
9.2 Scalability Architecture
Horizontal Scaling:
                   Load Balancer (NGINX)
                            │
        ┌───────────────────┼───────────────────┐
        ▼                   ▼                   ▼
   App Server 1       App Server 2       App Server 3
        │                   │                   │
        └───────────────────┼───────────────────┘
                            │
                    ┌───────┴───────┐
                    ▼               ▼
               MongoDB         Redis Cluster
              (Replica Set)   (Session Store)
Caching Strategy:
typescript
// Multi-layer caching
class CacheStrategy {
  // L1: In-memory (LRU)
  private memoryCache = new LRUCache({ max: 500 });
  
  // L2: Redis
  private redisCache: Redis;
  
  // L3: Database
  private db: MongoClient;
  
  async get(key: string): Promise<any> {
    // Try memory first
    const fromMemory = this.memoryCache.get(key);
    if (fromMemory) return fromMemory;
    
    // Try Redis
    const fromRedis = await this.redisCache.get(key);
    if (fromRedis) {
      this.memoryCache.set(key, fromRedis);
      return fromRedis;
    }
    
    // Fallback to database
    const fromDB = await this.db.findOne({ key });
    if (fromDB) {
      await this.redisCache.set(key, fromDB, 'EX', 3600);
      this.memoryCache.set(key, fromDB);
    }
    return fromDB;
  }
}
Database Sharding (Future):
javascript
// Shard by user ID hash
const shard = Math.floor(
  parseInt(userId.slice(-8), 16) % NUM_SHARDS
);
Message Queue for Async Tasks:
typescript
// Using Bull for background jobs
import Bull from 'bull';

const analyticsQueue = new Bull('analytics', {
  redis: redisConfig
});

analyticsQueue.process(async (job) => {
  await processAnalytics(job.data);
});

// Enqueue analytics job
await analyticsQueue.add({
  conversationId,
  metrics: { /* ... */ }
});
9.3 Monitoring & Observability
Logging Strategy:
typescript
import winston from 'winston';

const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.json()
  ),
  transports: [
    new winston.transports.File({ 
      filename: 'logs/error.log', 
      level: 'error' 
    }),
    new winston.transports.File({ 
      filename: 'logs/combined.log' 
    })
  ]
});

// Structured logging
logger.info('Message processed', {
  conversationId,
  userId,
  agent: 'DSA_Agent',
  latency: 2300,
  tokens: 450
});
Performance Metrics:
typescript
import prometheus from 'prom-client';

// Custom metrics
const messageLatency = new prometheus.Histogram({
  name: 'message_processing_duration_seconds',
  help: 'Time to process a message',
  labelNames: ['agent', 'subject']
});

const activeConnections = new prometheus.Gauge({
  name: 'websocket_active_connections',
  help: 'Number of active WebSocket connections'
});
Error Tracking (Sentry):
typescript
import * as Sentry from '@sentry/node';

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,
  tracesSampleRate: 0.1
});

// Capture LLM errors
Sentry.captureException(error, {
  tags: {
    agent: 'DSA_Agent',
    conversationId
  },
  extra: {
    prompt: sanitizedPrompt,
    response: sanitizedResponse
  }
});

10. Future RAG Integration
10.1 Architecture Extension
Current:  User Query → LangGraph → LLM → Response

With RAG: User Query → LangGraph → Retriever → Context + LLM → Response
                                       │
                                       ▼
                                  Vector DB
                               (Embeddings of
                                CS textbooks,
                                papers, docs)
10.2 Vector Database Setup
Technology Choice: Pinecone
typescript
import { PineconeClient } from '@pinecone-database/pinecone';

const pinecone = new PineconeClient();
await pinecone.init({
  apiKey: process.env.PINECONE_API_KEY,
  environment: process.env.PINECONE_ENV
});

// Create index
await pinecone.createIndex({
  name: 'cs-knowledge-base',
  dimension: 1536,        // OpenAI embedding size
  metric: 'cosine'
});
10.3 Document Ingestion Pipeline
typescript
interface DocumentIngestion {
  // 1. Extract text from PDFs
  extractPDF(file: Buffer): Promise<string>;
  
  // 2. Chunk text intelligently
  chunkText(text: string, options: {
    chunkSize: number;        // 500-1000 tokens
    overlap: number;          // 50-100 tokens
    preserveStructure: boolean;
  }): string[];
  
  // 3. Generate embeddings
  generateEmbeddings(chunks: string[]): Promise<number[][]>;
  
  // 4. Store in vector DB with metadata
  storeVectors(embeddings: number[][], metadata: {
    source: string;
    subject: string;
    page: number;
    chapter: string;
  }): Promise<void>;
}
10.4 Enhanced Agent with RAG
typescript
class RAGEnhancedAgent extends BaseAgent {
  async process(state: ConversationState) {
    // 1. Generate query embedding
    const queryEmbedding = await this.embedQuery(
      state.messages[state.messages.length - 1].content
    );
    
    // 2. Retrieve relevant context
    const context = await this.retriever.search({
      vector: queryEmbedding,
      topK: 5,
      filter: {
        subject: state.currentSubject
      }
    });
    
    // 3. Build enhanced prompt
    const prompt = this.buildRAGPrompt(
      state.messages,
      context
    );
    
    // 4. Generate response with context
    const response = await this.llm.generate(prompt);
    
    return {
      response,
      sources: context.map(c => c.metadata),
      confidence: this.calculateConfidence(context)
    };
  }
}
10.5 Knowledge Base Structure
knowledge_base/
├── algorithms/
│   ├── clrs_introduction_to_algorithms.pdf
│   ├── sedgewick_algorithms.pdf
│   └── leetcode_patterns.pdf
│
├── operating_systems/
│   ├── tanenbaum_modern_os.pdf
│   └── silberschatz_os_concepts.pdf
│
├── networks/
│   ├── kurose_ross_networking.pdf
│   └── tcp_ip_illustrated.pdf
│
├── databases/
│   ├── elmasri_navathe_databases.pdf
│   └── postgresql_documentation.pdf
│
└── software_engineering/
    ├── design_patterns_gang_of_four.pdf
    └── clean_code_martin.pdf
10.6 Hybrid Search Strategy
typescript
// Combine keyword search + semantic search
const hybridSearch = async (query: string) => {
  // Semantic search (vector similarity)
  const semanticResults = await vectorDB.search(
    await embedQuery(query),
    { topK: 10 }
  );
  
  // Keyword search (BM25)
  const keywordResults = await textSearch(query, {
    fields: ['title', 'content'],
    topK: 10
  });
  
  // Merge and re-rank
  return rerank(semanticResults, keywordResults, query);
};

11. Deployment Strategy
11.1 Environment Configuration
Development:
env
NODE_ENV=development
PORT=3000
MONGODB_URI=mongodb://localhost:27017/cs_chatbot_dev
REDIS_URL=redis://localhost:6379
ANTHROPIC_API_KEY=sk-ant-...
LOG_LEVEL=debug
Production:
env
NODE_ENV=production
PORT=8080
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/cs_chatbot
REDIS_URL=rediss://redis.example.com:6380
ANTHROPIC_API_KEY=sk-ant-...
LOG_LEVEL=info
SENTRY_DSN=https://...
11.2 Docker Setup
docker-compose.yml (Development):
yaml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    env_file:
      - ./backend/.env
    depends_on:
      - mongodb
      - redis
    volumes:
      - ./backend:/app
      - /app/node_modules

  frontend:
    build: ./frontend
    ports:
      - "5173:5173"
    env_file:
      - ./frontend/.env
    volumes:
      - ./frontend:/app
      - /app/node_modules

  mongodb:
    image: mongo:6.0
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

  redis:
    image: redis:7.2-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data

volumes:
  mongodb_data:
  redis_data:
11.3 CI/CD Pipeline (GitHub Actions)
yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '20'
      
      - name: Install dependencies
        run: |
          cd backend && npm ci
          cd ../frontend && npm ci
      
      - name: Run linter
        run: |
          cd backend && npm run lint
          cd ../frontend && npm run lint
      
      - name: Run tests
        run: |
          cd backend && npm test
          cd ../frontend && npm test

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Deploy to production
        run: |
          # Deploy commands (e.g., AWS, Vercel, Railway)

12. Success Metrics & KPIs
12.1 User Experience Metrics
Response Time: < 3 seconds (P95)
First Token Latency: < 500ms
Uptime: 99.9%
Error Rate: < 0.5%
12.2 Quality Metrics
User Satisfaction: > 4.0/5.0 average rating
Helpful Response Rate: > 85%
Follow-up Question Rate: < 30% (indicates clear answers)
Session Duration: 5-15 minutes (engaged learning)
12.3 Technical Metrics
Agent Routing Accuracy: > 90%
Cache Hit Rate: > 60%
API Cost per Query: < $0.05
Concurrent Users Supported: 1000+

13. Risk Mitigation
13.1 Identified Risks
Risk
Impact
Probability
Mitigation
LLM API downtime
High
Medium
Multi-provider fallback, cached responses
Database connection loss
High
Low
Replica sets, automatic reconnection
Rate limit exhaustion
Medium
High
Queue system, user tier limits
Incorrect answers
High
Medium
Confidence scoring, feedback loop
Security breach
Critical
Low
Regular audits, penetration testing
Cost overrun (API)
Medium
Medium
Budget alerts, response caching

13.2 Fallback Strategies
typescript
// Multi-provider LLM with fallback
class ResilientLLMService {
  async generate(prompt: string) {
    try {
      return await this.claudeProvider.generate(prompt);
    } catch (error) {
      logger.warn('Claude unavailable, falling back to OpenAI');
      try {
        return await this.openaiProvider.generate(prompt);
      } catch (secondError) {
        logger.error('All LLM providers unavailable');
        return this.getCachedResponse(prompt) || 
               this.getGenericFallback();
      }
    }
  }
}

14. Post-Launch Roadmap
Phase 1 (Months 1-2)
User feedback collection
A/B testing for response formats
Performance optimization based on real usage
Agent fine-tuning
Phase 2 (Months 3-4)
RAG implementation with CS textbooks
Multi-language support
Voice input/output
Mobile app development
Phase 3 (Months 5-6)
Personalized learning paths
Quiz generation
Collaborative study rooms
Integration with LMS platforms

15. Conclusion
This master plan provides a comprehensive blueprint for building a production-ready Student CS Chatbot system. The architecture is designed to be:
Scalable: Horizontal scaling, caching, load balancing
Maintainable: Clean code, TypeScript, comprehensive tests
Extensible: Modular agents, easy RAG integration
Reliable: Error handling, monitoring, fallbacks
Educational: Subject-specific expertise, clear explanations
Next Steps
Review & Approval: Validate architecture with stakeholders
Environment Setup: Provision development infrastructure
Sprint Planning: Break down Phase 1 into 2-week sprints
Code Generation: Begin systematic implementation
Iterative Development: Build, test, deploy, iterate

Document Version: 1.0
Last Updated: December 27, 2025
Author: Expert Developer & Architect
Status: Ready for Implementation
Artifacts
Download all
Master plan
Document · MD 
Incognito chat


