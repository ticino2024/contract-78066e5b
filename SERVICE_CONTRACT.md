# Service Contract: Social Media Analytics Dashboard

## Document Information
- **Service Name**: Social Media Analytics Dashboard
- **Version**: 1.0.0
- **Date**: 2025-10-28
- **Status**: Draft

---

## 1. Service Overview

### 1.1 Service Description
A comprehensive social media analytics platform that provides real-time data visualization, user engagement metrics, and content performance tracking across multiple social media platforms. The service enables businesses and content creators to make data-driven decisions through intuitive dashboards and actionable insights.

### 1.2 Service Objectives
- **Real-Time Monitoring**: Provide live updates on social media metrics with <5 second latency
- **Multi-Platform Support**: Aggregate data from Twitter/X, Facebook, Instagram, LinkedIn, and TikTok
- **Actionable Insights**: Generate AI-powered recommendations for content optimization
- **Performance Tracking**: Historical analysis with customizable date ranges and trend visualization
- **Competitive Analysis**: Benchmark performance against competitors and industry standards

### 1.3 Target Users
- **Content Creators**: Individual influencers and creators tracking engagement
- **Marketing Teams**: Corporate social media managers and marketing departments
- **Agencies**: Digital marketing agencies managing multiple client accounts
- **Analysts**: Data analysts requiring detailed performance reports

### 1.4 Key Features
- Real-time dashboard with live metric updates
- Multi-platform social media account integration
- Engagement metrics (likes, shares, comments, saves)
- Audience demographics and growth analytics
- Content performance ranking and comparison
- Sentiment analysis of comments and mentions
- Automated report generation (daily/weekly/monthly)
- Custom alerts and notifications
- Export capabilities (PDF, CSV, Excel)
- AI-powered content recommendations

---

## 2. System Architecture

### 2.1 High-Level Architecture

```mermaid
graph TB
    subgraph "Client Layer"
        A[Web Browser] --> B[React Frontend]
    end
    
    subgraph "API Gateway Layer"
        B --> C[API Gateway/Load Balancer]
    end
    
    subgraph "Application Layer"
        C --> D[FastAPI Backend]
        D --> E[Authentication Service]
        D --> F[Analytics Service]
        D --> G[Report Service]
        D --> H[AI Agent Service]
    end
    
    subgraph "Data Layer"
        F --> I[PostgreSQL]
        F --> J[Redis Cache]
        F --> K[TimescaleDB]
        H --> L[Vector DB]
    end
    
    subgraph "External Services"
        F --> M[Twitter API]
        F --> N[Facebook API]
        F --> O[Instagram API]
        F --> P[LinkedIn API]
        F --> Q[TikTok API]
        H --> R[OpenAI API]
    end
    
    subgraph "Background Processing"
        S[Celery Workers] --> I
        S --> K
        T[Data Collection Jobs] --> S
        U[Report Generation Jobs] --> S
    end
    
    subgraph "Monitoring"
        V[Prometheus] --> D
        V --> S
        W[Grafana] --> V
        X[ELK Stack] --> D
    end
```

### 2.2 Component Breakdown

#### Frontend Component
- **Framework**: React 18.x with TypeScript
- **UI Library**: Material-UI (MUI) v5
- **State Management**: Redux Toolkit with RTK Query
- **Charts**: Recharts + D3.js for advanced visualizations
- **Real-time**: Socket.io-client for WebSocket connections
- **Build Tool**: Vite

#### Backend Component
- **Framework**: FastAPI 0.104.x (Python 3.11+)
- **ORM**: SQLAlchemy 2.x with Alembic migrations
- **Validation**: Pydantic v2
- **Authentication**: JWT with OAuth2
- **API Documentation**: OpenAPI/Swagger auto-generated
- **WebSocket**: FastAPI WebSocket support

#### Agent Component
- **Framework**: LangChain 0.1.x
- **LLM**: OpenAI GPT-4 Turbo
- **Vector Store**: Pinecone or Chroma
- **Embeddings**: OpenAI text-embedding-3-small
- **Tools**: Custom tools for data analysis and recommendations

#### Background Processing
- **Task Queue**: Celery 5.x
- **Message Broker**: Redis 7.x
- **Scheduler**: Celery Beat for periodic tasks

### 2.3 Technology Stack

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| Frontend | React | 18.2+ | UI Framework |
| Frontend | TypeScript | 5.0+ | Type Safety |
| Frontend | Redux Toolkit | 2.0+ | State Management |
| Frontend | Material-UI | 5.14+ | Component Library |
| Frontend | Recharts | 2.8+ | Data Visualization |
| Backend | Python | 3.11+ | Programming Language |
| Backend | FastAPI | 0.104+ | Web Framework |
| Backend | SQLAlchemy | 2.0+ | ORM |
| Backend | Pydantic | 2.0+ | Data Validation |
| Database | PostgreSQL | 15+ | Primary Database |
| Database | TimescaleDB | 2.13+ | Time-Series Data |
| Database | Redis | 7.0+ | Caching & Queue |
| Agent | LangChain | 0.1+ | AI Agent Framework |
| Agent | OpenAI | 1.0+ | LLM Provider |
| Processing | Celery | 5.3+ | Task Queue |
| Monitoring | Prometheus | 2.47+ | Metrics Collection |
| Monitoring | Grafana | 10.0+ | Visualization |
| Logging | ELK Stack | 8.10+ | Log Aggregation |

### 2.4 Infrastructure Requirements

- **Compute**: 
  - Web Server: 4 vCPU, 16GB RAM (auto-scaling 2-8 instances)
  - Worker Nodes: 2 vCPU, 8GB RAM (auto-scaling 2-10 instances)
  
- **Storage**:
  - PostgreSQL: 500GB SSD with automatic backups
  - Redis: 32GB RAM with persistence
  - Object Storage: S3-compatible for reports and exports

- **Network**:
  - CDN for static assets
  - Load balancer with SSL termination
  - VPC with private subnets for databases

---

## 3. Frontend Specifications

### 3.1 UI/UX Requirements

#### Design Principles
- **Responsive**: Mobile-first design supporting desktop, tablet, and mobile
- **Accessible**: WCAG 2.1 AA compliance
- **Performance**: First Contentful Paint < 1.5s, Time to Interactive < 3s
- **Dark Mode**: Support for light/dark theme switching
- **Internationalization**: Support for English, Spanish, French, German

#### Visual Design
- Modern, clean interface with data-focused layouts
- Consistent color scheme aligned with branding
- Intuitive navigation with sidebar and top bar
- Card-based layout for metrics and charts
- Responsive grid system

### 3.2 Page Structure and Navigation

```mermaid
graph TD
    A[Login/Register] --> B[Dashboard Home]
    B --> C[Overview Dashboard]
    B --> D[Platform Analytics]
    B --> E[Content Performance]
    B --> F[Audience Insights]
    B --> G[Reports]
    B --> H[Settings]
    
    D --> D1[Twitter Analytics]
    D --> D2[Facebook Analytics]
    D --> D3[Instagram Analytics]
    D --> D4[LinkedIn Analytics]
    D --> D5[TikTok Analytics]
    
    E --> E1[Top Posts]
    E --> E2[Content Calendar]
    E --> E3[Sentiment Analysis]
    
    F --> F1[Demographics]
    F --> F2[Growth Trends]
    F --> F3[Engagement Patterns]
    
    G --> G1[Scheduled Reports]
    G --> G2[Custom Reports]
    G --> G3[Export Center]
    
    H --> H1[Account Settings]
    H --> H2[Connected Accounts]
    H --> H3[Billing]
    H --> H4[API Keys]
```

### 3.3 Key Pages

#### 3.3.1 Dashboard Home (`/dashboard`)
**Components**:
- `<MetricsSummaryCards />` - Key metrics overview (followers, engagement, reach)
- `<RealTimeActivityFeed />` - Live social media activity stream
- `<EngagementChart />` - 24-hour engagement trend
- `<TopPerformingContent />` - Top 5 posts by engagement
- `<PlatformComparison />` - Multi-platform performance comparison
- `<QuickActions />` - Shortcuts to common tasks
- `<AIRecommendations />` - AI-powered insights widget

#### 3.3.2 Platform Analytics (`/analytics/:platform`)
**Components**:
- `<PlatformSelector />` - Switch between platforms
- `<DateRangePicker />` - Custom date range selection
- `<FollowerGrowthChart />` - Time-series follower count
- `<EngagementMetricsGrid />` - Likes, comments, shares, saves
- `<PostFrequencyHeatmap />` - Posting patterns calendar
- `<AudienceActiveTimesChart />` - Best times to post
- `<HashtagPerformance />` - Top hashtags analysis

#### 3.3.3 Content Performance (`/content`)
**Components**:
- `<ContentTable />` - Sortable/filterable content list
- `<ContentTypeFilter />` - Filter by image, video, carousel, etc.
- `<PerformanceMetrics />` - Detailed metrics per post
- `<SentimentAnalysis />` - Comment sentiment visualization
- `<ContentComparison />` - Side-by-side post comparison
- `<ExportButton />` - Export content performance data

#### 3.3.4 Audience Insights (`/audience`)
**Components**:
- `<DemographicsChart />` - Age, gender, location breakdown
- `<GrowthTrendChart />` - Follower growth over time
- `<EngagementRateChart />` - Engagement rate trends
- `<TopFollowersTable />` - Most engaged followers
- `<AudienceInterestsCloud />` - Interest categories word cloud
- `<GeographicMap />` - Follower location map

#### 3.3.5 Reports (`/reports`)
**Components**:
- `<ReportTemplates />` - Pre-built report templates
- `<CustomReportBuilder />` - Drag-and-drop report creator
- `<ScheduledReportsList />` - Manage scheduled reports
- `<ReportHistory />` - Previous reports archive
- `<ExportOptions />` - PDF, Excel, CSV export

#### 3.3.6 Settings (`/settings`)
**Components**:
- `<ProfileSettings />` - User profile management
- `<ConnectedAccountsManager />` - OAuth connections to social platforms
- `<NotificationSettings />` - Alert preferences
- `<BillingInformation />` - Subscription and payment
- `<APIKeysManager />` - API key generation and management
- `<TeamMembers />` - Team collaboration settings

### 3.4 Component Hierarchy

```
App
├── AuthProvider
│   ├── LoginPage
│   └── RegisterPage
└── AppLayout
    ├── Sidebar
    │   ├── Logo
    │   ├── Navigation
    │   └── UserMenu
    ├── TopBar
    │   ├── Breadcrumbs
    │   ├── SearchBar
    │   ├── Notifications
    │   └── ProfileDropdown
    └── MainContent
        ├── DashboardRoutes
        │   ├── DashboardHome
        │   │   ├── MetricsSummaryCards
        │   │   ├── RealTimeActivityFeed
        │   │   ├── EngagementChart
        │   │   ├── TopPerformingContent
        │   │   └── AIRecommendations
        │   ├── PlatformAnalytics
        │   │   ├── PlatformSelector
        │   │   ├── DateRangePicker
        │   │   ├── MetricsGrid
        │   │   └── ChartsContainer
        │   ├── ContentPerformance
        │   ├── AudienceInsights
        │   ├── Reports
        │   └── Settings
        └── ToastNotifications
```

### 3.5 State Management Approach

#### Redux Store Structure
```typescript
{
  auth: {
    user: User | null,
    token: string | null,
    isAuthenticated: boolean,
    loading: boolean
  },
  dashboard: {
    metrics: MetricsSummary,
    realtimeActivity: Activity[],
    dateRange: DateRange,
    selectedPlatforms: Platform[]
  },
  analytics: {
    platformData: Record<Platform, PlatformAnalytics>,
    loading: boolean,
    error: string | null,
    lastUpdated: timestamp
  },
  content: {
    posts: Post[],
    filters: ContentFilters,
    sorting: SortOptions,
    pagination: PaginationState
  },
  audience: {
    demographics: Demographics,
    growth: GrowthData[],
    engagement: EngagementData[]
  },
  reports: {
    templates: ReportTemplate[],
    scheduled: ScheduledReport[],
    history: Report[]
  },
  settings: {
    connectedAccounts: ConnectedAccount[],
    notifications: NotificationSettings,
    theme: 'light' | 'dark'
  },
  ui: {
    sidebarOpen: boolean,
    loading: Record<string, boolean>,
    notifications: Notification[]
  }
}
```

#### API Integration Pattern
- **RTK Query** for all API calls with automatic caching
- **Optimistic Updates** for mutations
- **Polling** for real-time data (30-second intervals)
- **WebSocket** for live activity feed
- **Error Handling** with retry logic and user-friendly messages

---

## 4. Backend Specifications

### 4.1 API Endpoints and Methods

#### Authentication Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/v1/auth/register` | User registration | No |
| POST | `/api/v1/auth/login` | User login | No |
| POST | `/api/v1/auth/refresh` | Refresh access token | Yes (Refresh Token) |
| POST | `/api/v1/auth/logout` | User logout | Yes |
| POST | `/api/v1/auth/forgot-password` | Request password reset | No |
| POST | `/api/v1/auth/reset-password` | Reset password | No |
| GET | `/api/v1/auth/me` | Get current user | Yes |

#### Social Account Management

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/v1/accounts` | List connected accounts | Yes |
| POST | `/api/v1/accounts/connect` | Initiate OAuth connection | Yes |
| DELETE | `/api/v1/accounts/{account_id}` | Disconnect account | Yes |
| GET | `/api/v1/accounts/{account_id}/verify` | Verify account status | Yes |
| PUT | `/api/v1/accounts/{account_id}/refresh` | Refresh account data | Yes |

#### Dashboard & Metrics

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/v1/dashboard/summary` | Get dashboard summary metrics | Yes |
| GET | `/api/v1/dashboard/activity` | Real-time activity feed | Yes |
| GET | `/api/v1/dashboard/recommendations` | AI-powered recommendations | Yes |
| GET | `/api/v1/metrics/overview` | Overview metrics for date range | Yes |
| GET | `/api/v1/metrics/platform/{platform}` | Platform-specific metrics | Yes |
| GET | `/api/v1/metrics/compare` | Compare multiple platforms | Yes |

#### Analytics

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/v1/analytics/growth` | Follower growth data | Yes |
| GET | `/api/v1/analytics/engagement` | Engagement metrics | Yes |
| GET | `/api/v1/analytics/demographics` | Audience demographics | Yes |
| GET | `/api/v1/analytics/best-times` | Optimal posting times | Yes |
| GET | `/api/v1/analytics/hashtags` | Hashtag performance | Yes |
| GET | `/api/v1/analytics/sentiment` | Sentiment analysis | Yes |

#### Content Performance

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/v1/content/posts` | List posts with metrics | Yes |
| GET | `/api/v1/content/posts/{post_id}` | Get post details | Yes |
| GET | `/api/v1/content/top-performing` | Top performing content | Yes |
| GET | `/api/v1/content/compare` | Compare posts | Yes |
| POST | `/api/v1/content/analyze` | Analyze content performance | Yes |
| GET | `/api/v1/content/export` | Export content data | Yes |

#### Reports

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/v1/reports/templates` | List report templates | Yes |
| POST | `/api/v1/reports/generate` | Generate custom report | Yes |
| GET | `/api/v1/reports` | List user's reports | Yes |
| GET | `/api/v1/reports/{report_id}` | Get report details | Yes |
| POST | `/api/v1/reports/schedule` | Schedule recurring report | Yes |
| GET | `/api/v1/reports/scheduled` | List scheduled reports | Yes |
| PUT | `/api/v1/reports/scheduled/{id}` | Update scheduled report | Yes |
| DELETE | `/api/v1/reports/scheduled/{id}` | Delete scheduled report | Yes |
| GET | `/api/v1/reports/{report_id}/download` | Download report file | Yes |

#### AI Agent

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/v1/agent/chat` | Send message to AI agent | Yes |
| GET | `/api/v1/agent/conversations` | List conversations | Yes |
| GET | `/api/v1/agent/conversations/{id}` | Get conversation history | Yes |
| POST | `/api/v1/agent/analyze` | Request AI analysis | Yes |
| POST | `/api/v1/agent/recommendations` | Get content recommendations | Yes |

#### Settings & Admin

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/v1/settings/profile` | Get user profile | Yes |
| PUT | `/api/v1/settings/profile` | Update user profile | Yes |
| GET | `/api/v1/settings/notifications` | Get notification settings | Yes |
| PUT | `/api/v1/settings/notifications` | Update notification settings | Yes |
| GET | `/api/v1/settings/api-keys` | List API keys | Yes |
| POST | `/api/v1/settings/api-keys` | Create API key | Yes |
| DELETE | `/api/v1/settings/api-keys/{key_id}` | Revoke API key | Yes |
| GET | `/api/v1/settings/billing` | Get billing info | Yes |

#### WebSocket Endpoints

| Endpoint | Description | Auth Required |
|----------|-------------|---------------|
| `/ws/activity` | Real-time activity stream | Yes |
| `/ws/metrics` | Live metric updates | Yes |
| `/ws/agent` | AI agent chat stream | Yes |

### 4.2 Request/Response Schemas

#### Authentication

**POST /api/v1/auth/register**
```json
// Request
{
  "email": "user@example.com",
  "password": "SecurePass123!",
  "full_name": "John Doe",
  "company_name": "Acme Inc."
}

// Response (201 Created)
{
  "user": {
    "id": "usr_abc123",
    "email": "user@example.com",
    "full_name": "John Doe",
    "company_name": "Acme Inc.",
    "created_at": "2025-10-28T10:00:00Z"
  },
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "refresh_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "bearer",
  "expires_in": 3600
}
```

**POST /api/v1/auth/login**
```json
// Request
{
  "email": "user@example.com",
  "password": "SecurePass123!"
}

// Response (200 OK)
{
  "user": {
    "id": "usr_abc123",
    "email": "user@example.com",
    "full_name": "John Doe"
  },
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "refresh_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "bearer",
  "expires_in": 3600
}
```

#### Dashboard Summary

**GET /api/v1/dashboard/summary?date_range=7d**
```json
// Response (200 OK)
{
  "date_range": {
    "start": "2025-10-21T00:00:00Z",
    "end": "2025-10-28T23:59:59Z"
  },
  "total_followers": 125340,
  "follower_change": {
    "value": 2450,
    "percentage": 1.99
  },
  "total_engagement": 45680,
  "engagement_change": {
    "value": 3210,
    "percentage": 7.56
  },
  "total_reach": 2456000,
  "reach_change": {
    "value": 345000,
    "percentage": 16.34
  },
  "engagement_rate": 3.64,
  "platforms": [
    {
      "platform": "twitter",
      "followers": 45000,
      "engagement": 12500,
      "posts": 28
    },
    {
      "platform": "instagram",
      "followers": 52000,
      "engagement": 18900,
      "posts": 21
    },
    {
      "platform": "facebook",
      "followers": 18340,
      "engagement": 8900,
      "posts": 15
    },
    {
      "platform": "linkedin",
      "followers": 10000,
      "engagement": 5380,
      "posts": 12
    }
  ],
  "top_content": [
    {
      "id": "post_123",
      "platform": "instagram",
      "content_type": "image",
      "caption": "Amazing sunset view...",
      "engagement": 3450,
      "reach": 125000,
      "posted_at": "2025-10-26T18:30:00Z"
    }
  ]
}
```

#### Content Performance

**GET /api/v1/content/posts?platform=instagram&limit=50&offset=0**
```json
// Response (200 OK)
{
  "total": 234,
  "limit": 50,
  "offset": 0,
  "posts": [
    {
      "id": "post_123",
      "platform": "instagram",
      "platform_post_id": "ig_abc123",
      "content_type": "image",
      "caption": "Amazing sunset view from the mountains...",
      "media_urls": [
        "https://cdn.example.com/images/post_123.jpg"
      ],
      "posted_at": "2025-10-26T18:30:00Z",
      "metrics": {
        "likes": 2450,
        "comments": 187,
        "shares": 234,
        "saves": 579,
        "reach": 125000,
        "impressions": 156000,
        "engagement_rate": 2.23
      },
      "sentiment": {
        "positive": 0.82,
        "neutral": 0.15,
        "negative": 0.03
      },
      "hashtags": ["#sunset", "#mountains", "#nature"],
      "location": "Rocky Mountains, CO"
    }
  ]
}
```

#### Analytics - Demographics

**GET /api/v1/analytics/demographics?platform=instagram**
```json
// Response (200 OK)
{
  "platform": "instagram",
  "total_followers": 52000,
  "age_groups": [
    {"range": "13-17", "count": 2600, "percentage": 5.0},
    {"range": "18-24", "count": 15600, "percentage": 30.0},
    {"range": "25-34", "count": 20800, "percentage": 40.0},
    {"range": "35-44", "count": 10400, "percentage": 20.0},
    {"range": "45-54", "count": 2080, "percentage": 4.0},
    {"range": "55+", "count": 520, "percentage": 1.0}
  ],
  "gender": [
    {"type": "female", "count": 31200, "percentage": 60.0},
    {"type": "male", "count": 18720, "percentage": 36.0},
    {"type": "other", "count": 2080, "percentage": 4.0}
  ],
  "top_countries": [
    {"country": "US", "count": 26000, "percentage": 50.0},
    {"country": "UK", "count": 7800, "percentage": 15.0},
    {"country": "CA", "count": 5200, "percentage": 10.0},
    {"country": "AU", "count": 3120, "percentage": 6.0},
    {"country": "DE", "count": 2600, "percentage": 5.0}
  ],
  "top_cities": [
    {"city": "New York", "country": "US", "count": 5200},
    {"city": "Los Angeles", "country": "US", "count": 4160},
    {"city": "London", "country": "UK", "count": 3640},
    {"city": "Toronto", "country": "CA", "count": 2600},
    {"city": "Sydney", "country": "AU", "count": 2080}
  ]
}
```

#### AI Agent Chat

**POST /api/v1/agent/chat**
```json
// Request
{
  "conversation_id": "conv_abc123", // optional, null for new conversation
  "message": "What are my best performing posts this week?"
}

// Response (200 OK)
{
  "conversation_id": "conv_abc123",
  "message_id": "msg_xyz789",
  "response": "Based on your data from October 21-28, your top 3 performing posts are:\n\n1. Instagram post from Oct 26 (sunset photo) - 3,450 engagements, 2.23% engagement rate\n2. Twitter thread from Oct 24 (industry insights) - 2,890 engagements, 1.87% engagement rate\n3. LinkedIn article from Oct 23 - 1,540 engagements, 3.45% engagement rate\n\nThe sunset photo on Instagram had exceptional performance, with 579 saves indicating high-quality content. Would you like me to analyze what made it successful?",
  "suggested_actions": [
    "Analyze top post success factors",
    "Show engagement trends",
    "Get content recommendations"
  ],
  "timestamp": "2025-10-28T10:15:00Z"
}
```

### 4.3 Data Models and Relationships

#### Entity Relationship Diagram

```mermaid
erDiagram
    USER ||--o{ CONNECTED_ACCOUNT : has
    USER ||--o{ REPORT : generates
    USER ||--o{ API_KEY : owns
    USER ||--o{ NOTIFICATION_SETTING : configures
    USER ||--o{ CONVERSATION : has
    
    CONNECTED_ACCOUNT ||--o{ SOCIAL_POST : contains
    CONNECTED_ACCOUNT ||--o{ METRIC_SNAPSHOT : tracks
    CONNECTED_ACCOUNT ||--|| ACCOUNT_METADATA : has
    
    SOCIAL_POST ||--o{ POST_METRIC : has
    SOCIAL_POST ||--o{ COMMENT : has
    SOCIAL_POST ||--o{ HASHTAG : includes
    
    COMMENT ||--|| SENTIMENT : analyzed_as
    
    REPORT ||--o{ REPORT_SECTION : contains
    
    CONVERSATION ||--o{ MESSAGE : contains

    USER {
        uuid id PK
        string email UK
        string password_hash
        string full_name
        string company_name
        timestamp created_at
        timestamp updated_at
        timestamp last_login
        boolean is_active
        string subscription_tier
    }
    
    CONNECTED_ACCOUNT {
        uuid id PK
        uuid user_id FK
        string platform
        string platform_user_id
        string platform_username
        string access_token_encrypted
        string refresh_token_encrypted
        timestamp token_expires_at
        json account_metadata
        boolean is_active
        timestamp connected_at
        timestamp last_synced_at
    }
    
    ACCOUNT_METADATA {
        uuid id PK
        uuid connected_account_id FK
        int follower_count
        int following_count
        string profile_image_url
        string bio
        string website_url
        json additional_info
        timestamp updated_at
    }
    
    SOCIAL_POST {
        uuid id PK
        uuid connected_account_id FK
        string platform
        string platform_post_id UK
        string content_type
        text caption
        jsonb media_urls
        jsonb hashtags
        string location
        timestamp posted_at
        timestamp created_at
        timestamp updated_at
    }
    
    POST_METRIC {
        uuid id PK
        uuid post_id FK
        int likes
        int comments
        int shares
        int saves
        int reach
        int impressions
        float engagement_rate
        timestamp recorded_at
    }
    
    COMMENT {
        uuid id PK
        uuid post_id FK
        string platform_comment_id
        string author_username
        text content
        timestamp posted_at
        int likes
        timestamp created_at
    }
    
    SENTIMENT {
        uuid id PK
        uuid comment_id FK
        float positive_score
        float neutral_score
        float negative_score
        string overall_sentiment
        timestamp analyzed_at
    }
    
    HASHTAG {
        uuid id PK
        string tag UK
        int usage_count
        timestamp first_used_at
        timestamp last_used_at
    }
    
    METRIC_SNAPSHOT {
        uuid id PK
        uuid connected_account_id FK
        string metric_type
        float value
        json metadata
        timestamp recorded_at
    }
    
    REPORT {
        uuid id PK
        uuid user_id FK
        string title
        string report_type
        json configuration
        string status
        string file_url
        timestamp generated_at
        timestamp expires_at
    }
    
    REPORT_SECTION {
        uuid id PK
        uuid report_id FK
        string section_type
        int order
        json data
    }
    
    API_KEY {
        uuid id PK
        uuid user_id FK
        string key_hash
        string key_prefix
        string name
        jsonb permissions
        timestamp created_at
        timestamp last_used_at
        timestamp expires_at
        boolean is_active
    }
    
    NOTIFICATION_SETTING {
        uuid id PK
        uuid user_id FK
        string notification_type
        boolean email_enabled
        boolean push_enabled
        json thresholds
    }
    
    CONVERSATION {
        uuid id PK
        uuid user_id FK
        string title
        timestamp created_at
        timestamp updated_at
    }
    
    MESSAGE {
        uuid id PK
        uuid conversation_id FK
        string role
        text content
        json metadata
        timestamp created_at
    }
```

### 4.4 Database Schema Design

#### Users Table
```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    company_name VARCHAR(255),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    last_login TIMESTAMP WITH TIME ZONE,
    is_active BOOLEAN DEFAULT true,
    subscription_tier VARCHAR(50) DEFAULT 'free',
    
    CONSTRAINT valid_email CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$')
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_created_at ON users(created_at);
```

#### Connected Accounts Table
```sql
CREATE TABLE connected_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    platform VARCHAR(50) NOT NULL,
    platform_user_id VARCHAR(255) NOT NULL,
    platform_username VARCHAR(255) NOT NULL,
    access_token_encrypted TEXT NOT NULL,
    refresh_token_encrypted TEXT,
    token_expires_at TIMESTAMP WITH TIME ZONE,
    account_metadata JSONB DEFAULT '{}',
    is_active BOOLEAN DEFAULT true,
    connected_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    last_synced_at TIMESTAMP WITH TIME ZONE,
    
    CONSTRAINT unique_platform_account UNIQUE(user_id, platform, platform_user_id),
    CONSTRAINT valid_platform CHECK (platform IN ('twitter', 'facebook', 'instagram', 'linkedin', 'tiktok'))
);

CREATE INDEX idx_connected_accounts_user_id ON connected_accounts(user_id);
CREATE INDEX idx_connected_accounts_platform ON connected_accounts(platform);
CREATE INDEX idx_connected_accounts_last_synced ON connected_accounts(last_synced_at);
```

#### Social Posts Table
```sql
CREATE TABLE social_posts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    connected_account_id UUID NOT NULL REFERENCES connected_accounts(id) ON DELETE CASCADE,
    platform VARCHAR(50) NOT NULL,
    platform_post_id VARCHAR(255) NOT NULL,
    content_type VARCHAR(50) NOT NULL,
    caption TEXT,
    media_urls JSONB DEFAULT '[]',
    hashtags JSONB DEFAULT '[]',
    location VARCHAR(255),
    posted_at TIMESTAMP WITH TIME ZONE NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    
    CONSTRAINT unique_platform_post UNIQUE(platform, platform_post_id),
    CONSTRAINT valid_content_type CHECK (content_type IN ('image', 'video', 'carousel', 'text', 'link', 'story'))
);

CREATE INDEX idx_social_posts_account ON social_posts(connected_account_id);
CREATE INDEX idx_social_posts_posted_at ON social_posts(posted_at DESC);
CREATE INDEX idx_social_posts_platform ON social_posts(platform);
CREATE INDEX idx_social_posts_hashtags ON social_posts USING GIN(hashtags);
```

#### Post Metrics Table (TimescaleDB)
```sql
CREATE TABLE post_metrics (
    id UUID DEFAULT gen_random_uuid(),
    post_id UUID NOT NULL REFERENCES social_posts(id) ON DELETE CASCADE,
    likes INTEGER DEFAULT 0,
    comments INTEGER DEFAULT 0,
    shares INTEGER DEFAULT 0,
    saves INTEGER DEFAULT 0,
    reach INTEGER DEFAULT 0,
    impressions INTEGER DEFAULT 0,
    engagement_rate DECIMAL(5,2) DEFAULT 0.0,
    recorded_at TIMESTAMP WITH TIME ZONE NOT NULL,
    
    PRIMARY KEY (id, recorded_at)
);

-- Convert to TimescaleDB hypertable
SELECT create_hypertable('post_metrics', 'recorded_at');

CREATE INDEX idx_post_metrics_post_id ON post_metrics(post_id, recorded_at DESC);
```

#### Metric Snapshots Table (TimescaleDB)
```sql
CREATE TABLE metric_snapshots (
    id UUID DEFAULT gen_random_uuid(),
    connected_account_id UUID NOT NULL REFERENCES connected_accounts(id) ON DELETE CASCADE,
    metric_type VARCHAR(100) NOT NULL,
    value DECIMAL(15,2) NOT NULL,
    metadata JSONB DEFAULT '{}',
    recorded_at TIMESTAMP WITH TIME ZONE NOT NULL,
    
    PRIMARY KEY (id, recorded_at)
);

-- Convert to TimescaleDB hypertable
SELECT create_hypertable('metric_snapshots', 'recorded_at');

CREATE INDEX idx_metric_snapshots_account ON metric_snapshots(connected_account_id, recorded_at DESC);
CREATE INDEX idx_metric_snapshots_type ON metric_snapshots(metric_type, recorded_at DESC);
```

### 4.5 Authentication and Authorization

#### JWT Token Structure
```json
{
  "sub": "usr_abc123",
  "email": "user@example.com",
  "subscription_tier": "pro",
  "iat": 1698480000,
  "exp": 1698483600,
  "type": "access"
}
```

#### Authorization Levels
- **Free Tier**: 3 connected accounts, 30-day data retention, basic reports
- **Pro Tier**: 10 connected accounts, 1-year data retention, advanced analytics, scheduled reports
- **Enterprise Tier**: Unlimited accounts, unlimited retention, API access, white-label reports

#### OAuth 2.0 Flow
1. User initiates connection to social platform
2. Backend generates OAuth authorization URL
3. User redirects to platform for authentication
4. Platform redirects back with authorization code
5. Backend exchanges code for access/refresh tokens
6. Tokens encrypted and stored in database
7. Background job starts data synchronization

### 4.6 Business Logic Requirements

#### Data Collection Logic
- **Initial Sync**: Fetch up to 90 days of historical data
- **Incremental Sync**: Poll for new content every 15 minutes
- **Metrics Update**: Update metrics for recent posts every 30 minutes
- **Account Metadata**: Refresh follower counts every hour
- **Rate Limiting**: Respect platform API rate limits with exponential backoff

#### Engagement Rate Calculation
```
engagement_rate = (likes + comments + shares + saves) / reach * 100
```

#### Sentiment Analysis Logic
- Analyze all comments using NLP model
- Categorize as positive (>0.6), neutral (0.4-0.6), or negative (<0.4)
- Calculate overall post sentiment as weighted average
- Update sentiment scores daily for recent posts

#### Best Posting Time Algorithm
1. Group historical posts by day of week and hour
2. Calculate average engagement rate for each time slot
3. Weight recent data (last 30 days) more heavily
4. Identify top 5 time slots per platform
5. Consider audience timezone distribution

#### Content Recommendation Engine
- Analyze top 10% performing posts by engagement rate
- Extract common patterns (content type, caption length, hashtags, posting time)
- Compare with recent underperforming posts
- Generate specific, actionable recommendations
- Update recommendations weekly

---

## 5. Agent Specifications

### 5.1 Agent Purpose and Capabilities

#### Primary Purpose
Provide intelligent, conversational analytics insights and content recommendations through natural language interaction.

#### Core Capabilities
1. **Data Analysis**: Query and analyze social media metrics conversationally
2. **Trend Identification**: Identify patterns and trends in engagement data
3. **Content Recommendations**: Suggest optimal content strategies
4. **Performance Comparison**: Compare content performance across platforms
5. **Anomaly Detection**: Alert users to unusual metric changes
6. **Report Generation**: Generate custom reports based on natural language requests
7. **Competitive Intelligence**: Provide industry benchmarking insights

### 5.2 Agent Architecture

```mermaid
graph TD
    A[User Input] --> B[Agent Orchestrator]
    B --> C[Intent Classifier]
    C --> D{Intent Type}
    
    D -->|Query Metrics| E[Metrics Tool]
    D -->|Analyze Content| F[Content Analysis Tool]
    D -->|Get Recommendations| G[Recommendation Tool]
    D -->|Generate Report| H[Report Tool]
    D -->|Compare Data| I[Comparison Tool]
    
    E --> J[PostgreSQL Query]
    F --> J
    G --> K[ML Model]
    H --> L[Report Service]
    I --> J
    
    J --> M[Context Builder]
    K --> M
    L --> M
    
    M --> N[LLM (GPT-4)]
    N --> O[Response Generator]
    O --> P[Formatted Response]
    
    P --> Q[Vector Store]
    Q --> B
```

### 5.3 LangChain Implementation

#### Agent Configuration
```python
from langchain.agents import AgentExecutor, OpenAIFunctionsAgent
from langchain.chat_models import ChatOpenAI
from langchain.memory import ConversationBufferMemory
from langchain.prompts import MessagesPlaceholder

# Initialize LLM
llm = ChatOpenAI(
    model="gpt-4-turbo-preview",
    temperature=0.2,
    max_tokens=2000
)

# System prompt
system_message = """You are a social media analytics expert assistant. 
You help users understand their social media performance and provide 
actionable insights to improve their content strategy.

You have access to tools to:
- Query engagement metrics across platforms
- Analyze content performance
- Generate recommendations
- Create custom reports
- Compare data across time periods

Always provide specific, data-driven insights with numbers and percentages.
When making recommendations, explain the reasoning based on the data.
Be concise but comprehensive. Use formatting for better readability."""

# Memory for conversation context
memory = ConversationBufferMemory(
    memory_key="chat_history",
    return_messages=True
)

# Create agent
agent = OpenAIFunctionsAgent(
    llm=llm,
    tools=tools,
    system_message=system_message,
    memory=memory
)

agent_executor = AgentExecutor(
    agent=agent,
    tools=tools,
    memory=memory,
    verbose=True,
    max_iterations=5
)
```

### 5.4 Custom Tools

#### 1. Metrics Query Tool
```python
from langchain.tools import BaseTool
from pydantic import BaseModel, Field

class MetricsQueryInput(BaseModel):
    platform: str = Field(description="Social media platform: twitter, instagram, facebook, linkedin, tiktok, or 'all'")
    metric_type: str = Field(description="Metric type: followers, engagement, reach, impressions")
    date_range: str = Field(description="Date range: 7d, 30d, 90d, or custom format YYYY-MM-DD:YYYY-MM-DD")
    
class MetricsQueryTool(BaseTool):
    name = "query_metrics"
    description = """Query social media metrics for a specific platform and time period.
    Returns numerical data about followers, engagement, reach, or impressions."""
    args_schema = MetricsQueryInput
    
    def _run(self, platform: str, metric_type: str, date_range: str) -> dict:
        # Implementation queries database
        # Returns structured metric data
        pass
```

#### 2. Content Analysis Tool
```python
class ContentAnalysisInput(BaseModel):
    content_ids: list[str] = Field(description="List of content IDs to analyze")
    analysis_type: str = Field(description="Type: performance, sentiment, comparison")

class ContentAnalysisTool(BaseTool):
    name = "analyze_content"
    description = """Analyze specific posts or content performance.
    Can analyze engagement patterns, sentiment, or compare multiple posts."""
    args_schema = ContentAnalysisInput
    
    def _run(self, content_ids: list[str], analysis_type: str) -> dict:
        # Implementation analyzes content metrics
        # Returns analysis results
        pass
```

#### 3. Recommendation Tool
```python
class RecommendationInput(BaseModel):
    focus_area: str = Field(description="Area for recommendations: posting_times, content_type, hashtags, overall")
    platform: str = Field(description="Platform to optimize for")

class RecommendationTool(BaseTool):
    name = "get_recommendations"
    description = """Generate AI-powered recommendations for improving social media performance.
    Analyzes historical data to suggest optimal strategies."""
    args_schema = RecommendationInput
    
    def _run(self, focus_area: str, platform: str) -> dict:
        # Implementation uses ML model
        # Returns recommendations
        pass
```

#### 4. Comparison Tool
```python
class ComparisonInput(BaseModel):
    comparison_type: str = Field(description="Type: platforms, time_periods, content")
    params: dict = Field(description="Comparison parameters")

class ComparisonTool(BaseTool):
    name = "compare_data"
    description = """Compare metrics across platforms, time periods, or different content.
    Useful for trend analysis and performance evaluation."""
    args_schema = ComparisonInput
    
    def _run(self, comparison_type: str, params: dict) -> dict:
        # Implementation compares data
        # Returns comparison results
        pass
```

#### 5. Report Generation Tool
```python
class ReportGenerationInput(BaseModel):
    report_type: str = Field(description="Report type: summary, detailed, custom")
    date_range: str = Field(description="Date range for report")
    platforms: list[str] = Field(description="Platforms to include")
    sections: list[str] = Field(description="Sections to include")

class ReportGenerationTool(BaseTool):
    name = "generate_report"
    description = """Generate a custom analytics report based on specified parameters.
    Creates downloadable PDF or Excel reports."""
    args_schema = ReportGenerationInput
    
    def _run(self, report_type: str, date_range: str, platforms: list[str], sections: list[str]) -> dict:
        # Implementation generates report
        # Returns report URL
        pass
```

### 5.5 Conversation Examples

#### Example 1: Performance Query
```
User: "How did my Instagram posts perform last week?"

Agent Process:
1. Intent Classification: Query Metrics
2. Tool Selection: query_metrics + analyze_content
3. Execution: Fetch Instagram data for last 7 days
4. Response Generation:

Agent: "Your Instagram performance last week (Oct 21-28):

📊 Key Metrics:
- Total Posts: 8
- Total Engagement: 18,900 (↑12% vs previous week)
- Average Engagement Rate: 2.45%
- Total Reach: 425,000
- New Followers: 1,240

🏆 Top Performing Post:
Your sunset photo on Oct 26 received 3,450 engagements (2.23% rate) with exceptional save rate (579 saves).

💡 Insight: Posts with scenic photography are performing 34% better than product posts this week."
```

#### Example 2: Content Recommendation
```
User: "What should I post next on Twitter to maximize engagement?"

Agent Process:
1. Intent Classification: Get Recommendations
2. Tool Selection: get_recommendations + query_metrics
3. Execution: Analyze Twitter historical data
4. Response Generation:

Agent: "Based on your Twitter performance data, here are my recommendations:

🎯 Optimal Posting Time: Tuesday or Thursday between 2-4 PM EST
Your audience is most active during these windows (avg engagement rate: 2.87% vs your overall 1.92%)

✍️ Content Type: Twitter Threads (3-5 tweets)
Your threads perform 42% better than single tweets. Recent industry insights thread got 2,890 engagements.

#️⃣ Hashtags: Use 2-3 relevant hashtags
Sweet spot is 2-3 hashtags. Posts with 2 hashtags have 23% higher engagement than posts with 5+.

📝 Suggested Topics (based on your top performers):
1. Industry analysis/insights (avg. 2,450 engagements)
2. Behind-the-scenes content (avg. 1,980 engagements)
3. Data visualizations (avg. 1,750 engagements)

Would you like me to analyze any specific topic for potential performance?"
```

#### Example 3: Comparative Analysis
```
User: "Compare my Instagram and TikTok performance this month"

Agent Process:
1. Intent Classification: Compare Data
2. Tool Selection: compare_data + query_metrics
3. Execution: Fetch and compare platform data
4. Response Generation:

Agent: "Here's your Instagram vs TikTok comparison for October:

📱 Instagram:
- Posts: 21
- Total Engagement: 52,400
- Avg. Engagement Rate: 2.34%
- Follower Growth: +2,840 (5.8%)
- Best Content: Photos with captions

📱 TikTok:
- Posts: 15
- Total Engagement: 87,600
- Avg. Engagement Rate: 5.67%
- Follower Growth: +4,120 (12.3%)
- Best Content: Short tutorials

🔑 Key Insights:
1. TikTok has 2.4x higher engagement rate despite fewer posts
2. TikTok drives faster follower growth (12.3% vs 5.8%)
3. Instagram posts get more saves (great for long-term value)
4. TikTok videos under 30 seconds perform best

💡 Recommendation: Consider repurposing your top Instagram content into TikTok format to maximize cross-platform reach."
```

### 5.6 Integration Points

#### Backend Integration
- **Authentication**: Use same JWT tokens as main API
- **Database Access**: Read-only access to analytics database
- **API Calls**: Can trigger report generation and data exports
- **WebSocket**: Stream responses for real-time chat experience

#### External Service Integration
- **OpenAI API**: GPT-4 for natural language understanding and generation
- **Vector Database**: Store conversation history and context embeddings
- **ML Service**: Custom recommendation models for content optimization

### 5.7 Error Handling

```python
# Tool execution error handling
try:
    result = tool.run(input_params)
except RateLimitError:
    return "I'm experiencing high demand. Please try again in a moment."
except DataNotFoundError:
    return "I couldn't find data for that request. Could you check the date range or platform name?"
except PermissionError:
    return "You don't have access to that data. Please connect the relevant social media account first."
except Exception as e:
    logger.error(f"Agent tool error: {str(e)}")
    return "I encountered an issue processing your request. Our team has been notified."
```

### 5.8 Performance Optimization

- **Response Streaming**: Stream LLM responses token-by-token for better UX
- **Tool Result Caching**: Cache frequent queries (Redis) with 5-minute TTL
- **Parallel Tool Execution**: Execute independent tools concurrently
- **Context Window Management**: Keep conversation context under 8K tokens
- **Embedding Cache**: Cache embedded queries for semantic similarity search

---

## 6. Data Models (Detailed)

### 6.1 Core Entity Definitions

#### User Entity
```typescript
interface User {
  id: string; // UUID
  email: string; // Unique, validated email
  password_hash: string; // bcrypt hashed
  full_name: string;
  company_name?: string;
  profile_image_url?: string;
  created_at: Date;
  updated_at: Date;
  last_login?: Date;
  is_active: boolean;
  is_verified: boolean;
  subscription_tier: 'free' | 'pro' | 'enterprise';
  subscription_expires_at?: Date;
  timezone: string; // IANA timezone
  language: string; // ISO 639-1 code
}

// Validation Rules
const UserValidation = {
  email: z.string().email().max(255),
  password: z.string().min(12).max(128).regex(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])/),
  full_name: z.string().min(2).max(255),
  company_name: z.string().max(255).optional(),
  timezone: z.string().refine(isValidTimezone),
  language: z.enum(['en', 'es', 'fr', 'de', 'pt', 'it'])
};
```

#### Connected Account Entity
```typescript
interface ConnectedAccount {
  id: string; // UUID
  user_id: string; // Foreign key to User
  platform: 'twitter' | 'facebook' | 'instagram' | 'linkedin' | 'tiktok';
  platform_user_id: string; // User ID on the platform
  platform_username: string;
  platform_display_name: string;
  access_token_encrypted: string; // AES-256 encrypted
  refresh_token_encrypted?: string;
  token_expires_at?: Date;
  account_metadata: AccountMetadata;
  is_active: boolean;
  connected_at: Date;
  last_synced_at?: Date;
  sync_status: 'idle' | 'syncing' | 'error';
  sync_error_message?: string;
}

interface AccountMetadata {
  follower_count: number;
  following_count: number;
  post_count: number;
  profile_image_url: string;
  bio: string;
  website_url?: string;
  verified: boolean;
  account_type: 'personal' | 'business' | 'creator';
  platform_specific: Record<string, any>;
}
```

#### Social Post Entity
```typescript
interface SocialPost {
  id: string; // UUID
  connected_account_id: string; // Foreign key
  platform: string;
  platform_post_id: string; // Unique per platform
  content_type: 'image' | 'video' | 'carousel' | 'text' | 'link' | 'story' | 'reel';
  caption?: string;
  media_urls: MediaItem[];
  hashtags: string[];
  mentions: string[];
  location?: Location;
  posted_at: Date;
  is_promoted: boolean;
  parent_post_id?: string; // For threads/replies
  created_at: Date;
  updated_at: Date;
}

interface MediaItem {
  url: string;
  type: 'image' | 'video' | 'gif';
  thumbnail_url?: string;
  width?: number;
  height?: number;
  duration?: number; // seconds for videos
}

interface Location {
  name: string;
  latitude?: number;
  longitude?: number;
  city?: string;
  country?: string;
}
```

#### Post Metrics Entity (Time-Series)
```typescript
interface PostMetric {
  id: string; // UUID
  post_id: string; // Foreign key
  likes: number;
  comments: number;
  shares: number;
  saves: number;
  reach: number; // Unique views
  impressions: number; // Total views
  engagement_rate: number; // Calculated percentage
  video_views?: number;
  video_completion_rate?: number;
  click_through_rate?: number;
  recorded_at: Date; // Timestamp for time-series
}

// Calculated Fields
interface CalculatedMetrics {
  engagement_rate: number; // (likes + comments + shares + saves) / reach * 100
  virality_score: number; // shares / reach * 100
  save_rate: number; // saves / reach * 100
  comment_rate: number; // comments / reach * 100
}
```

#### Comment Entity
```typescript
interface Comment {
  id: string; // UUID
  post_id: string; // Foreign key
  platform_comment_id: string;
  author_username: string;
  author_display_name: string;
  author_profile_url: string;
  content: string;
  posted_at: Date;
  likes: number;
  reply_to_comment_id?: string; // For nested comments
  is_verified_author: boolean;
  created_at: Date;
}
```

#### Sentiment Analysis Entity
```typescript
interface Sentiment {
  id: string; // UUID
  comment_id: string; // Foreign key
  positive_score: number; // 0.0 - 1.0
  neutral_score: number; // 0.0 - 1.0
  negative_score: number; // 0.0 - 1.0
  overall_sentiment: 'positive' | 'neutral' | 'negative';
  confidence: number; // 0.0 - 1.0
  keywords: string[]; // Extracted keywords
  analyzed_at: Date;
  model_version: string;
}
```

#### Metric Snapshot Entity (Time-Series)
```typescript
interface MetricSnapshot {
  id: string; // UUID
  connected_account_id: string; // Foreign key
  metric_type: 'followers' | 'engagement' | 'reach' | 'impressions' | 'engagement_rate';
  value: number;
  change_from_previous: number;
  change_percentage: number;
  metadata: Record<string, any>;
  recorded_at: Date;
}
```

#### Report Entity
```typescript
interface Report {
  id: string; // UUID
  user_id: string; // Foreign key
  title: string;
  report_type: 'summary' | 'detailed' | 'custom' | 'scheduled';
  configuration: ReportConfiguration;
  status: 'pending' | 'generating' | 'completed' | 'failed';
  file_url?: string;
  file_format: 'pdf' | 'excel' | 'csv';
  generated_at?: Date;
  expires_at?: Date; // Auto-delete after 30 days
  created_at: Date;
}

interface ReportConfiguration {
  date_range: {
    start: Date;
    end: Date;
  };
  platforms: string[];
  sections: ReportSection[];
  include_charts: boolean;
  include_raw_data: boolean;
  branding?: {
    logo_url: string;
    company_name: string;
    color_scheme: string;
  };
}

type ReportSection = 
  | 'executive_summary'
  | 'platform_overview'
  | 'engagement_metrics'
  | 'audience_demographics'
  | 'top_content'
  | 'growth_analysis'
  | 'recommendations';
```

#### Scheduled Report Entity
```typescript
interface ScheduledReport {
  id: string; // UUID
  user_id: string; // Foreign key
  title: string;
  report_configuration: ReportConfiguration;
  schedule: CronExpression; // e.g., "0 9 * * 1" for Monday 9 AM
  timezone: string;
  recipients: string[]; // Email addresses
  is_active: boolean;
  last_generated_at?: Date;
  next_generation_at: Date;
  created_at: Date;
  updated_at: Date;
}
```

#### API Key Entity
```typescript
interface APIKey {
  id: string; // UUID
  user_id: string; // Foreign key
  key_hash: string; // SHA-256 hash
  key_prefix: string; // First 8 chars for identification
  name: string;
  permissions: Permission[];
  rate_limit: number; // Requests per hour
  is_active: boolean;
  created_at: Date;
  last_used_at?: Date;
  expires_at?: Date;
}

interface Permission {
  resource: 'metrics' | 'content' | 'analytics' | 'reports';
  actions: ('read' | 'write' | 'delete')[];
}
```

#### Notification Setting Entity
```typescript
interface NotificationSetting {
  id: string; // UUID
  user_id: string; // Foreign key
  notification_type: 'milestone' | 'anomaly' | 'report_ready' | 'weekly_summary';
  email_enabled: boolean;
  push_enabled: boolean;
  in_app_enabled: boolean;
  thresholds?: {
    follower_milestone?: number[];
    engagement_drop_percentage?: number;
    reach_threshold?: number;
  };
  quiet_hours?: {
    start: string; // "22:00"
    end: string; // "08:00"
  };
}
```

#### Conversation Entity (AI Agent)
```typescript
interface Conversation {
  id: string; // UUID
  user_id: string; // Foreign key
  title: string;
  created_at: Date;
  updated_at: Date;
  message_count: number;
  metadata: {
    topics: string[];
    platforms_discussed: string[];
  };
}

interface Message {
  id: string; // UUID
  conversation_id: string; // Foreign key
  role: 'user' | 'assistant' | 'system';
  content: string;
  metadata?: {
    tool_calls?: ToolCall[];
    suggested_actions?: string[];
    data_references?: string[];
  };
  created_at: Date;
}

interface ToolCall {
  tool_name: string;
  input_params: Record<string, any>;
  output: any;
  execution_time_ms: number;
}
```

### 6.2 Relationships Summary

```
User (1) ━━━ (N) ConnectedAccount
User (1) ━━━ (N) Report
User (1) ━━━ (N) ScheduledReport
User (1) ━━━ (N) APIKey
User (1) ━━━ (N) NotificationSetting
User (1) ━━━ (N) Conversation

ConnectedAccount (1) ━━━ (N) SocialPost
ConnectedAccount (1) ━━━ (N) MetricSnapshot

SocialPost (1) ━━━ (N) PostMetric
SocialPost (1) ━━━ (N) Comment

Comment (1) ━━━ (1) Sentiment

Conversation (1) ━━━ (N) Message
```

### 6.3 Indexes for Performance

```sql
-- User indexes
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_subscription ON users(subscription_tier, is_active);

-- Connected accounts indexes
CREATE INDEX idx_ca_user_platform ON connected_accounts(user_id, platform);
CREATE INDEX idx_ca_last_synced ON connected_accounts(last_synced_at) WHERE is_active = true;

-- Social posts indexes
CREATE INDEX idx_posts_account_date ON social_posts(connected_account_id, posted_at DESC);
CREATE INDEX idx_posts_platform_date ON social_posts(platform, posted_at DESC);
CREATE INDEX idx_posts_hashtags ON social_posts USING GIN(hashtags);

-- Post metrics indexes (TimescaleDB)
CREATE INDEX idx_metrics_post_time ON post_metrics(post_id, recorded_at DESC);

-- Metric snapshots indexes (TimescaleDB)
CREATE INDEX idx_snapshots_account_type_time ON metric_snapshots(connected_account_id, metric_type, recorded_at DESC);

-- Comments indexes
CREATE INDEX idx_comments_post ON comments(post_id, posted_at DESC);

-- Reports indexes
CREATE INDEX idx_reports_user_created ON reports(user_id, created_at DESC);
CREATE INDEX idx_reports_status ON reports(status) WHERE status IN ('pending', 'generating');
```

---

## 7. API Specifications (Extended)

### 7.1 Authentication Flow

#### Registration Flow
```
POST /api/v1/auth/register
  ↓
[Validate input]
  ↓
[Hash password]
  ↓
[Create user record]
  ↓
[Send verification email]
  ↓
[Generate JWT tokens]
  ↓
Return {user, access_token, refresh_token}
```

#### OAuth Connection Flow
```
POST /api/v1/accounts/connect
  ↓
[Generate OAuth state token]
  ↓
Return {authorization_url, state}
  ↓
[User authorizes on platform]
  ↓
GET /api/v1/accounts/callback?code=...&state=...
  ↓
[Validate state token]
  ↓
[Exchange code for tokens]
  ↓
[Encrypt and store tokens]
  ↓
[Trigger initial sync job]
  ↓
Return {connected_account}
```

### 7.2 Error Response Format

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request parameters",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ],
    "request_id": "req_abc123",
    "timestamp": "2025-10-28T10:15:00Z"
  }
}
```

### 7.3 Standard Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| `VALIDATION_ERROR` | 400 | Invalid request parameters |
| `AUTHENTICATION_REQUIRED` | 401 | Missing or invalid authentication |
| `INSUFFICIENT_PERMISSIONS` | 403 | User lacks required permissions |
| `RESOURCE_NOT_FOUND` | 404 | Requested resource doesn't exist |
| `RATE_LIMIT_EXCEEDED` | 429 | Too many requests |
| `INTERNAL_ERROR` | 500 | Unexpected server error |
| `SERVICE_UNAVAILABLE` | 503 | Temporary service outage |
| `PLATFORM_API_ERROR` | 502 | External platform API error |

### 7.4 Rate Limiting

| Tier | Requests per Hour | Burst Limit |
|------|------------------|-------------|
| Free | 100 | 10/minute |
| Pro | 1,000 | 50/minute |
| Enterprise | 10,000 | 200/minute |
| API Key | Configurable | Configurable |

**Rate Limit Headers**:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 87
X-RateLimit-Reset: 1698483600
```

### 7.5 Pagination

**Query Parameters**:
- `limit`: Number of items per page (max 100)
- `offset`: Number of items to skip
- `cursor`: Alternative cursor-based pagination

**Response Format**:
```json
{
  "data": [...],
  "pagination": {
    "total": 234,
    "limit": 50,
    "offset": 0,
    "has_more": true,
    "next_cursor": "eyJpZCI6ImFiYzEyMyJ9"
  }
}
```

### 7.6 Filtering and Sorting

**Query Parameters**:
```
GET /api/v1/content/posts?
  platform=instagram&
  content_type=image,video&
  date_from=2025-10-01&
  date_to=2025-10-28&
  min_engagement=1000&
  sort=engagement_rate&
  order=desc&
  limit=50
```

**Supported Sort Fields**:
- `posted_at`, `engagement_rate`, `likes`, `comments`, `shares`, `reach`

### 7.7 WebSocket Protocol

#### Connection
```javascript
const ws = new WebSocket('wss://api.example.com/ws/activity');
ws.send(JSON.stringify({
  type: 'authenticate',
  token: 'eyJhbGciOiJIUzI1NiIs...'
}));
```

#### Message Format
```json
{
  "type": "activity_update",
  "data": {
    "platform": "instagram",
    "activity_type": "new_post",
    "post": {
      "id": "post_123",
      "caption": "New product launch...",
      "posted_at": "2025-10-28T10:30:00Z"
    }
  },
  "timestamp": "2025-10-28T10:30:05Z"
}
```

#### Message Types
- `activity_update`: New social media activity
- `metric_update`: Real-time metric change
- `notification`: System notification
- `agent_response`: AI agent streaming response

---

## 8. Non-Functional Requirements

### 8.1 Performance Requirements

#### Response Time Targets
- **API Endpoints**: 
  - Simple queries: < 200ms (p95)
  - Complex analytics: < 1s (p95)
  - Report generation: < 30s
- **Dashboard Load**: 
  - Initial page load: < 2s
  - Subsequent navigation: < 500ms
- **Real-time Updates**: 
  - WebSocket latency: < 5s
  - Metric refresh: Every 30s

#### Throughput
- **Concurrent Users**: Support 1,000 concurrent users
- **API Requests**: Handle 1,000 requests/second
- **Background Jobs**: Process 10,000 jobs/hour

#### Database Performance
- **Query Performance**: 95% of queries < 100ms
- **Index Usage**: All queries must use indexes
- **Connection Pool**: 50-200 connections per instance

### 8.2 Security Requirements

#### Authentication & Authorization
- **Password Policy**: Minimum 12 characters, complexity requirements
- **JWT Expiration**: Access tokens 1 hour, refresh tokens 30 days
- **Session Management**: Automatic logout after 7 days inactivity
- **MFA**: Optional two-factor authentication
- **OAuth Security**: Use state parameter, validate redirect URIs

#### Data Protection
- **Encryption at Rest**: AES-256 for sensitive data (tokens, passwords)
- **Encryption in Transit**: TLS 1.3 for all API communication
- **Token Storage**: Encrypted OAuth tokens with key rotation
- **PII Protection**: Hash email addresses in logs
- **Data Anonymization**: Remove PII from analytics aggregates

#### API Security
- **Rate Limiting**: Prevent abuse and DDoS
- **Input Validation**: Validate all inputs with Pydantic
- **SQL Injection**: Use parameterized queries only
- **XSS Protection**: Sanitize all user-generated content
- **CSRF Protection**: Use CSRF tokens for state-changing operations
- **CORS**: Whitelist allowed origins

#### Compliance
- **GDPR**: Right to access, deletion, data portability
- **CCPA**: California Consumer Privacy Act compliance
- **SOC 2**: Type II certification (target)
- **Data Retention**: User-configurable retention policies
- **Audit Logs**: Log all data access and modifications

### 8.3 Scalability Requirements

#### Horizontal Scaling
- **Web Servers**: Auto-scale 2-8 instances based on CPU/memory
- **Worker Nodes**: Auto-scale 2-10 instances based on queue depth
- **Database**: Read replicas for analytics queries
- **Caching**: Distributed Redis cluster

#### Vertical Scaling
- **Database**: Support up to 5TB of data
- **Time-Series Data**: TimescaleDB compression for old data
- **Object Storage**: Unlimited report and media storage

#### Data Partitioning
- **User Sharding**: Partition users by ID range
- **Time-Series Partitioning**: Monthly partitions for metrics
- **Archive Strategy**: Move data >1 year to cold storage

### 8.4 Availability & Reliability

#### Uptime Targets
- **Service Availability**: 99.9% uptime (43 minutes downtime/month)
- **API Availability**: 99.95% uptime
- **Scheduled Maintenance**: < 4 hours/month, announced 7 days in advance

#### Disaster Recovery
- **Backup Frequency**: 
  - Database: Every 6 hours
  - Full backup: Daily
  - Point-in-time recovery: 7 days
- **Recovery Time Objective (RTO)**: < 4 hours
- **Recovery Point Objective (RPO)**: < 6 hours
- **Geographic Redundancy**: Multi-region deployment

#### Fault Tolerance
- **Database Failover**: Automatic failover to standby
- **Service Redundancy**: Multiple instances behind load balancer
- **Graceful Degradation**: Continue core functions during partial outage
- **Circuit Breakers**: Prevent cascade failures

### 8.5 Monitoring & Logging

#### Metrics Collection
- **Application Metrics**: Response times, error rates, throughput
- **Infrastructure Metrics**: CPU, memory, disk, network
- **Business Metrics**: Active users, API calls, report generations
- **Custom Metrics**: Platform sync status, AI agent usage

#### Logging Strategy
```
Level: INFO | ERROR | WARNING | DEBUG
Format: JSON structured logging
Retention: 30 days (hot), 1 year (cold)
Volume: ~100GB/day expected

Log Categories:
- api.request: API request/response
- api.error: API errors
- auth.login: Authentication events
- platform.sync: Social media sync jobs
- agent.query: AI agent interactions
- report.generation: Report generation
```

#### Alerting
- **Critical Alerts** (Immediate - PagerDuty):
  - Service down (>5% error rate)
  - Database unavailable
  - Payment processing failure
  
- **Warning Alerts** (Email - 15 min):
  - High response times (>2s p95)
  - Platform API failures
  - Queue backup (>1000 pending jobs)
  
- **Info Alerts** (Slack - 1 hour):
  - Unusual traffic patterns
  - High resource usage (>80%)

#### Dashboards
- **Operations Dashboard**: Service health, error rates, throughput
- **Business Dashboard**: Active users, usage metrics, revenue
- **Platform Dashboard**: Sync status, API quotas, error rates
- **Performance Dashboard**: Response times, database queries, cache hit rates

### 8.6 Testing Requirements

#### Unit Testing
- **Coverage Target**: >80% code coverage
- **Framework**: pytest for backend, Jest for frontend
- **Execution**: Run on every commit (CI/CD)

#### Integration Testing
- **API Testing**: Test all endpoints with realistic data
- **Database Testing**: Test migrations and queries
- **Platform Integration**: Mock external API responses
- **Execution**: Run on every PR

#### End-to-End Testing
- **User Flows**: Test critical user journeys
- **Framework**: Playwright for browser automation
- **Scenarios**:
  - User registration and login
  - Connect social media account
  - View dashboard and analytics
  - Generate and download report
- **Execution**: Run nightly

#### Performance Testing
- **Load Testing**: Simulate 1,000 concurrent users
- **Stress Testing**: Find breaking point
- **Endurance Testing**: Run at peak load for 24 hours
- **Tools**: k6, JMeter
- **Frequency**: Before major releases

#### Security Testing
- **Vulnerability Scanning**: Automated OWASP Top 10 checks
- **Penetration Testing**: Quarterly external pen test
- **Dependency Scanning**: Check for vulnerable dependencies
- **Tools**: Snyk, OWASP ZAP

### 8.7 Deployment Requirements

#### Continuous Integration/Deployment
```yaml
CI/CD Pipeline:
1. Code pushed to Git
2. Run linters and formatters
3. Run unit tests
4. Build Docker images
5. Run integration tests
6. Deploy to staging
7. Run E2E tests
8. Manual approval for production
9. Deploy to production (blue-green)
10. Run smoke tests
11. Monitor for errors
```

#### Infrastructure as Code
- **Tool**: Terraform for AWS resources
- **Version Control**: All infrastructure code in Git
- **Environments**: Development, Staging, Production
- **Configuration**: Environment variables, no hardcoded secrets

#### Release Strategy
- **Versioning**: Semantic versioning (MAJOR.MINOR.PATCH)
- **Release Frequency**: Weekly releases (Thursdays)
- **Hotfix Process**: Emergency fixes deployed within 4 hours
- **Rollback**: Automatic rollback if error rate >5%

#### Database Migrations
- **Tool**: Alembic for schema migrations
- **Strategy**: Forward-only migrations
- **Validation**: Test migrations on staging with production snapshot
- **Rollback Plan**: Keep previous schema version compatible

### 8.8 Documentation Requirements

#### API Documentation
- **Format**: OpenAPI 3.0 specification
- **Auto-Generation**: Generated from code annotations
- **Interactive**: Swagger UI for testing
- **Examples**: Request/response examples for all endpoints

#### User Documentation
- **Getting Started Guide**: Account setup and first dashboard
- **Platform Guides**: How to connect each social media platform
- **Feature Documentation**: Detailed guides for each feature
- **Video Tutorials**: Screen recordings for common tasks
- **FAQ**: Common questions and troubleshooting

#### Developer Documentation
- **Architecture Guide**: System design and component interaction
- **API Integration Guide**: How to use the public API
- **Webhook Guide**: Setting up and handling webhooks
- **Code Examples**: Sample code in Python, JavaScript, cURL

#### Operational Documentation
- **Runbook**: Incident response procedures
- **Deployment Guide**: How to deploy updates
- **Monitoring Guide**: Understanding metrics and alerts
- **Disaster Recovery**: Backup and restore procedures

---

## 9. Implementation Phases

### Phase 1: MVP (Weeks 1-6)
**Goal**: Core analytics dashboard with single platform support

**Backend**:
- User authentication and authorization
- OAuth integration for Instagram
- Basic data sync from Instagram API
- Core API endpoints (auth, accounts, metrics)
- PostgreSQL + Redis setup

**Frontend**:
- User registration and login
- Account connection flow
- Basic dashboard with key metrics
- Simple data visualization (charts)
- Responsive layout

**Deliverables**:
- Users can register and login
- Connect Instagram account
- View follower growth and engagement metrics
- See top performing posts

### Phase 2: Multi-Platform (Weeks 7-10)
**Goal**: Add support for all major platforms

**Backend**:
- OAuth for Twitter, Facebook, LinkedIn, TikTok
- Platform-specific data adapters
- Multi-platform data aggregation
- Enhanced API endpoints

**Frontend**:
- Platform selector
- Multi-platform comparison view
- Platform-specific analytics pages
- Enhanced visualizations

**Deliverables**:
- Support for 5 major platforms
- Compare performance across platforms
- Platform-specific insights

### Phase 3: Advanced Analytics (Weeks 11-14)
**Goal**: Deep analytics and insights

**Backend**:
- Sentiment analysis implementation
- Audience demographics aggregation
- Best posting time algorithm
- Content performance ranking
- TimescaleDB for time-series data

**Frontend**:
- Audience insights page
- Content performance page
- Sentiment analysis visualization
- Advanced filtering and sorting
- Date range selector

**Deliverables**:
- Detailed audience demographics
- Sentiment analysis of comments
- Content performance tracking
- Posting time recommendations

### Phase 4: AI Agent (Weeks 15-18)
**Goal**: Conversational AI analytics assistant

**Backend**:
- LangChain agent implementation
- Custom tools for data analysis
- Vector database for context
- Streaming response support

**Frontend**:
- AI chat interface
- Conversation history
- Suggested prompts
- Action buttons for recommendations

**Deliverables**:
- Conversational analytics queries
- AI-powered recommendations
- Natural language insights

### Phase 5: Reports & Automation (Weeks 19-22)
**Goal**: Automated reporting and alerts

**Backend**:
- Report generation service
- PDF/Excel export
- Scheduled report system (Celery)
- Notification system
- Email service integration

**Frontend**:
- Report builder interface
- Report templates
- Scheduled reports management
- Notification preferences

**Deliverables**:
- Custom report generation
- Scheduled automated reports
- Email notifications
- Export capabilities

### Phase 6: Polish & Scale (Weeks 23-26)
**Goal**: Production readiness and optimization

**Backend**:
- Performance optimization
- Caching layer enhancement
- Rate limiting implementation
- Security audit
- Load testing

**Frontend**:
- Performance optimization
- Accessibility audit (WCAG 2.1)
- Dark mode
- Internationalization (i18n)
- Mobile optimization

**Deliverables**:
- Production-ready system
- Performance benchmarks met
- Security compliance
- Full documentation

---

## 10. Technical Constraints & Assumptions

### 10.1 Constraints

#### Platform API Limitations
- **Rate Limits**: Must respect each platform's API rate limits
- **Data Access**: Limited to data accessible via public APIs
- **Historical Data**: Limited lookback period (typically 90 days)
- **Real-time**: Not truly real-time, 15-30 minute sync intervals

#### Technical Limitations
- **Browser Support**: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **Mobile**: iOS 13+, Android 8+
- **Database**: PostgreSQL 15+ required for JSON features
- **Python**: Python 3.11+ required for performance

#### Regulatory Constraints
- **Data Privacy**: GDPR, CCPA compliance required
- **Data Residency**: EU data must stay in EU regions
- **Terms of Service**: Must comply with platform ToS
- **Data Usage**: No unauthorized data selling or sharing

### 10.2 Assumptions

#### User Assumptions
- Users have social media accounts to connect
- Users grant necessary permissions for data access
- Users understand basic social media metrics
- Users have modern web browsers

#### Technical Assumptions
- Platform APIs remain stable and documented
- OAuth 2.0 continues to be the standard
- Cloud infrastructure (AWS/GCP) is available
- Third-party services (OpenAI) remain accessible

#### Business Assumptions
- Freemium model with paid tiers
- Monthly subscription pricing
- Annual pricing discount available
- Enterprise custom pricing

### 10.3 Dependencies

#### External Services
- **Social Media APIs**: Twitter, Facebook, Instagram, LinkedIn, TikTok
- **LLM Provider**: OpenAI API
- **Email Service**: SendGrid or AWS SES
- **CDN**: CloudFlare or AWS CloudFront
- **Object Storage**: AWS S3 or compatible
- **Payment Processing**: Stripe

#### Third-Party Libraries
- **Frontend**: React, Redux, Material-UI, Recharts, D3.js
- **Backend**: FastAPI, SQLAlchemy, Celery, LangChain
- **Database**: PostgreSQL, TimescaleDB, Redis
- **Monitoring**: Prometheus, Grafana, ELK Stack

---

## 11. Success Criteria

### 11.1 Technical Success Metrics

- **System Uptime**: ≥ 99.9%
- **API Response Time**: p95 < 200ms
- **Error Rate**: < 0.1%
- **Test Coverage**: ≥ 80%
- **Security Vulnerabilities**: Zero critical/high severity issues
- **Load Capacity**: Support 1,000 concurrent users

### 11.2 User Success Metrics

- **User Activation**: 80% of registered users connect ≥1 account
- **Retention**: 40% of users return after 7 days
- **Engagement**: Average 3 sessions per week per active user
- **Feature Adoption**: 60% of users use AI agent within first month
- **Report Generation**: Average 2 reports per user per month

### 11.3 Business Success Metrics

- **Conversion Rate**: 15% free to paid conversion
- **Customer Satisfaction**: NPS ≥ 40
- **Support Tickets**: < 5% of users create tickets monthly
- **Platform Coverage**: Support 5 major social platforms
- **API Reliability**: 99.95% successful platform API calls

---

## 12. Glossary

| Term | Definition |
|------|------------|
| **Engagement Rate** | (Likes + Comments + Shares + Saves) / Reach × 100 |
| **Reach** | Number of unique users who saw the content |
| **Impressions** | Total number of times content was viewed |
| **Virality Score** | Shares / Reach × 100 |
| **Save Rate** | Saves / Reach × 100 |
| **Follower Growth Rate** | (New Followers / Total Followers) × 100 |
| **Sentiment Score** | Positive sentiment (0-1 scale) minus negative sentiment |
| **Engagement** | Total interactions (likes + comments + shares + saves) |
| **Content Type** | Format of post (image, video, carousel, text, story) |
| **Posting Cadence** | Frequency of posts per week/month |
| **Peak Hours** | Times when audience is most active |
| **OAuth** | Open Authorization protocol for secure API access |
| **JWT** | JSON Web Token for authentication |
| **Time-Series Data** | Data indexed by timestamp for trend analysis |
| **Hypertable** | TimescaleDB table optimized for time-series data |

---

## 13. Appendix

### 13.1 Platform API References

- **Twitter API**: https://developer.twitter.com/en/docs
- **Facebook Graph API**: https://developers.facebook.com/docs/graph-api
- **Instagram Graph API**: https://developers.facebook.com/docs/instagram-api
- **LinkedIn API**: https://docs.microsoft.com/en-us/linkedin/
- **TikTok API**: https://developers.tiktok.com/

### 13.2 Technology Documentation

- **FastAPI**: https://fastapi.tiangolo.com/
- **React**: https://react.dev/
- **LangChain**: https://python.langchain.com/
- **PostgreSQL**: https://www.postgresql.org/docs/
- **TimescaleDB**: https://docs.timescale.com/
- **Redis**: https://redis.io/docs/

### 13.3 Sample Environment Variables

```bash
# Application
APP_NAME=social-media-analytics
APP_ENV=production
DEBUG=false
SECRET_KEY=<random-secret>

# Database
DATABASE_URL=postgresql://user:pass@host:5432/dbname
REDIS_URL=redis://host:6379/0

# Platform OAuth
TWITTER_CLIENT_ID=<client-id>
TWITTER_CLIENT_SECRET=<client-secret>
FACEBOOK_APP_ID=<app-id>
FACEBOOK_APP_SECRET=<app-secret>
INSTAGRAM_CLIENT_ID=<client-id>
INSTAGRAM_CLIENT_SECRET=<client-secret>

# External Services
OPENAI_API_KEY=<api-key>
SENDGRID_API_KEY=<api-key>
AWS_ACCESS_KEY_ID=<access-key>
AWS_SECRET_ACCESS_KEY=<secret-key>
AWS_S3_BUCKET=<bucket-name>

# Security
JWT_SECRET_KEY=<random-secret>
JWT_ALGORITHM=HS256
JWT_ACCESS_TOKEN_EXPIRE_MINUTES=60
ENCRYPTION_KEY=<32-byte-key>

# Monitoring
SENTRY_DSN=<sentry-dsn>
PROMETHEUS_PORT=9090
```

---

## Document Approval

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Product Owner | | | |
| Technical Lead | | | |
| Engineering Manager | | | |
| Security Officer | | | |

---

**Document Version**: 1.0.0  
**Last Updated**: 2025-10-28  
**Next Review**: 2025-11-28  
**Status**: Ready for Implementation
