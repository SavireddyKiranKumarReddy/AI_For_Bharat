# Dukaan AI

> AI-Powered Pricing & Inventory Intelligence Platform for Marketplace Sellers

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-in%20development-yellow.svg)]()

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Problem Statement](#problem-statement)
- [Solution Architecture](#solution-architecture)
- [Technology Stack](#technology-stack)
- [Core Capabilities](#core-capabilities)
- [System Requirements](#system-requirements)
- [Getting Started](#getting-started)
- [Documentation](#documentation)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

**Dukaan AI** is an enterprise-grade, AI-powered pricing and inventory intelligence platform designed to help small-to-medium marketplace sellers optimize their pricing strategies and inventory decisions. By leveraging machine learning, real-time data analytics, and automated workflows, Dukaan AI empowers sellers to stay competitive, maximize profits, and minimize stockouts across multiple e-commerce marketplaces.

### Vision

To democratize advanced pricing intelligence and inventory optimization for marketplace sellers of all sizes, enabling data-driven decision-making that was previously accessible only to large enterprises.

## ✨ Key Features

### 🔍 Competitive Intelligence
- **Multi-Marketplace Monitoring**: Track competitor prices across Amazon, eBay, and Shopify in real-time
- **Price Change Alerts**: Instant notifications when competitors adjust pricing by >5%
- **Historical Analysis**: 90-day price history with trend detection and volatility analysis
- **Competitor Discovery**: Automatic identification of up to 3+ competitors per product

### 💰 Dynamic Pricing Engine
- **AI-Driven Recommendations**: Smart pricing suggestions based on competition, demand, inventory, and margins
- **Multiple Strategies**: Support for competitive, premium, and clearance pricing approaches
- **Profit Margin Protection**: Never recommend prices below configured minimum margins
- **Inventory-Aware Pricing**: Automatic adjustments based on stock levels (preserve low stock, accelerate high stock)

### 📊 Demand Forecasting
- **Time Series Analysis**: Predict demand for 7, 14, and 30-day horizons
- **Seasonality Detection**: Identify and incorporate seasonal patterns automatically
- **External Event Integration**: Adjust forecasts for holidays, promotions, and special events
- **Accuracy Tracking**: Continuous model improvement with 80%+ forecast accuracy

### 📦 Inventory Optimization
- **Smart Reorder Points**: Calculate optimal reorder timing based on demand, lead time, and safety stock
- **Economic Order Quantity**: Minimize total costs (holding + ordering)
- **Stockout Prediction**: High-priority alerts for predicted stockouts within 7 days
- **Safety Stock Calculation**: Statistical approach (1.65σ) for optimal buffer inventory

### 📈 Real-Time Analytics Dashboard
- **Live Data**: Updates within 5 minutes of market changes
- **Comprehensive Metrics**: Prices, margins, inventory levels, and competitor positions
- **Trend Visualization**: 7-day comparative analysis with percentage changes
- **Advanced Filtering**: By marketplace, category, and custom date ranges
- **Responsive Design**: Full functionality on desktop, tablet, and mobile devices

### 🔔 Intelligent Alerts & Insights
- **Multi-Channel Notifications**: Email, SMS, webhooks, and in-dashboard alerts
- **Priority-Based Routing**: Severity-based alert delivery (low, medium, high)
- **Actionable Insights**: Revenue-impact prioritized recommendations
- **Custom Webhooks**: Integrate with existing tools and workflows

### 🔐 Enterprise Security
- **End-to-End Encryption**: TLS 1.3 for data in transit, AES-256 for data at rest
- **Multi-Factor Authentication**: TOTP and SMS-based 2FA
- **Role-Based Access Control**: Admin, Manager, and Viewer roles with granular permissions
- **Comprehensive Audit Logs**: 1-year retention of all data access and modifications

## 🎯 Problem Statement

Marketplace sellers face critical challenges that directly impact profitability:

1. **Manual Price Monitoring**: Tracking competitor prices across multiple marketplaces is time-consuming and error-prone
2. **Reactive Pricing**: Sellers often discover price changes too late, losing sales to competitors
3. **Inventory Mismanagement**: Stockouts lead to lost revenue; overstock ties up capital
4. **Lack of Demand Visibility**: Without forecasting, sellers can't optimize inventory or pricing
5. **Data Overload**: Too much data, not enough actionable insights
6. **Limited Resources**: Small sellers lack access to enterprise-grade analytics tools

### Business Impact

- **Lost Revenue**: Uncompetitive pricing and stockouts cost sellers 15-30% of potential revenue
- **Wasted Time**: Manual monitoring consumes 10-15 hours per week
- **Poor Margins**: Reactive pricing often leads to unnecessary discounting
- **Capital Inefficiency**: Excess inventory ties up 20-40% more capital than necessary

## 💡 Solution Architecture

Dukaan AI addresses these challenges through a modern, scalable microservices architecture:

```
┌─────────────────────────────────────────────────────────────┐
│                     Client Layer                            │
│              Web Dashboard  |  Mobile App                   │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                   API Gateway / Load Balancer               │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                  Application Services                       │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │ Price Monitor│  │Pricing Engine│  │Forecast Engine│      │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │Alert Service │  │  Auth Service│  │  Integration │       │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│              Message Queue (RabbitMQ/Kafka)                 │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                      Data Layer                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │  Price DB    │  │  Sales DB    │  │   User DB    │       │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
│                    ┌──────────────┐                         │
│                    │ Redis Cache  │                         │
│                    └──────────────┘                         │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                   External Services                         │
│        Amazon API  |  eBay API  |  Shopify API              │
└─────────────────────────────────────────────────────────────┘
```

### Design Principles

1. **Modularity**: Separate concerns into distinct, independently scalable services
2. **Real-Time Processing**: Event-driven architecture for immediate insights and alerts
3. **Scalability**: Horizontal scaling to support growing user base and data volume
4. **Data Integrity**: Consistency across distributed components with ACID guarantees
5. **Security First**: Encryption, authentication, and authorization at every layer
6. **Testability**: Property-based testing ensures correctness across all scenarios

## 🛠 Technology Stack

### Backend Services
- **Runtime**: Node.js / TypeScript
- **API Framework**: Express.js / Fastify
- **Message Queue**: RabbitMQ / Apache Kafka
- **Caching**: Redis
- **Authentication**: JWT + OAuth 2.0

### Data Layer
- **Primary Database**: PostgreSQL (relational data)
- **Time Series**: TimescaleDB (price history, metrics)
- **Document Store**: MongoDB (flexible schemas)

### Machine Learning
- **Forecasting**: Prophet / ARIMA / LSTM models
- **Price Optimization**: Reinforcement Learning
- **Pattern Detection**: Scikit-learn / TensorFlow

### Frontend
- **Framework**: React / Next.js
- **State Management**: Redux / Zustand
- **UI Components**: Material-UI / Tailwind CSS
- **Charts**: Recharts / D3.js

### Infrastructure
- **Container Orchestration**: Kubernetes
- **CI/CD**: GitHub Actions / GitLab CI
- **Monitoring**: Prometheus + Grafana
- **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana)

### External Integrations
- **Amazon**: MWS / SP-API
- **eBay**: Trading API
- **Shopify**: Admin API
- **Notifications**: SendGrid (email), Twilio (SMS)

## 🚀 Core Capabilities

### 1. Price Monitoring Service

**Responsibilities:**
- Poll marketplace APIs every 15 minutes for competitor prices
- Detect price changes and calculate deltas
- Store 90-day historical price data
- Emit real-time price change events

**Key Metrics:**
- Update frequency: 15 minutes
- Alert latency: <1 minute for >5% price changes
- Competitor coverage: 3+ per product
- API retry policy: 3 attempts with exponential backoff

### 2. Pricing Engine Service

**Responsibilities:**
- Generate AI-driven pricing recommendations
- Apply configurable pricing strategies
- Calculate price elasticity
- Enforce profit margin constraints

**Pricing Strategies:**
- **Competitive**: Within 5% of median competitor price
- **Premium**: 10-20% above median competitor price
- **Clearance**: Optimized for rapid inventory liquidation

**Constraints:**
- Never recommend below minimum profit margin
- Adjust for low inventory (<20% avg): increase price
- Adjust for high inventory (>150% avg): decrease price

### 3. Forecast Engine Service

**Responsibilities:**
- Predict product demand using time series analysis
- Detect seasonal patterns automatically
- Incorporate external events (holidays, promotions)
- Calculate and track forecast accuracy

**Forecast Horizons:**
- 7-day: Short-term tactical decisions
- 14-day: Medium-term planning
- 30-day: Long-term strategic planning

**Accuracy Targets:**
- Confidence intervals: 80%+ accuracy
- Continuous model improvement via feedback loops
- Minimum data requirement: 90 days historical sales

### 4. Inventory Optimizer

**Responsibilities:**
- Calculate optimal reorder points
- Recommend economic order quantities
- Predict stockout risks
- Optimize safety stock levels

**Optimization Approach:**
- Reorder point = (Demand × Lead Time) + Safety Stock
- Safety stock = 1.65 × σ (demand during lead time)
- EOQ minimizes total cost (holding + ordering)
- High-priority alerts for stockouts within 7 days

### 5. Alert Service

**Responsibilities:**
- Process events from all services
- Apply configurable alert rules
- Deliver notifications via multiple channels
- Manage user preferences and quiet hours

**Alert Types:**
- **Price Undercut**: Competitor undercuts by >10%
- **Margin Warning**: Profit margin below threshold
- **Stockout Risk**: Predicted stockout within 7 days
- **Pricing Opportunity**: Competitor price increase >5%

**Delivery Channels:**
- Email (SendGrid)
- SMS (Twilio)
- Webhooks (custom integrations)
- In-dashboard notifications

### 6. Marketplace Integration Service

**Responsibilities:**
- Handle OAuth 2.0 authentication with marketplaces
- Execute price updates via marketplace APIs
- Manage rate limiting and retries
- Securely store and refresh API credentials

**Supported Marketplaces:**
- **Amazon**: MWS / SP-API
- **eBay**: Trading API
- **Shopify**: Admin API

**Security:**
- AES-256 encryption for stored credentials
- Automatic token refresh before expiration
- Rate limit compliance with exponential backoff

## 📊 System Requirements

### Performance Targets

| Metric | Target | Measurement |
|--------|--------|-------------|
| Dashboard Load Time | <2 seconds | p95 |
| Pricing Recommendation | <5 seconds per SKU | Average |
| Demand Forecast | <10 seconds per SKU | Average |
| API Response Time | <500ms | p95 |
| System Uptime | 99.5% | Monthly |
| Concurrent Users | 100+ | Without degradation |

### Scalability

- **Horizontal Scaling**: Auto-scale at 80% capacity
- **Data Retention**: 90 days price history, 1 year audit logs
- **Product Capacity**: 10,000+ SKUs per seller
- **Report Generation**: <30 seconds for 10,000 records

### Security Requirements

- **Encryption**: TLS 1.3 (transit), AES-256 (rest)
- **Authentication**: Password complexity + MFA
- **Session Management**: 30-minute inactivity timeout
- **Audit Logging**: All data access and modifications
- **Compliance**: GDPR, CCPA ready

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ and npm/yarn
- PostgreSQL 14+
- Redis 7+
- Docker & Docker Compose (recommended)
- Marketplace API credentials (Amazon, eBay, Shopify)

### Installation

```bash
# Clone the repository
git clone https://github.com/SavireddyKiranKumarReddy/dukaan-ai.git
cd dukaan-ai

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Set up database
npm run db:migrate
npm run db:seed

# Start development server
npm run dev
```

### Docker Setup (Recommended)

```bash
# Build and start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

### Configuration

Create a `.env` file with the following variables:

```env
# Application
NODE_ENV=development
PORT=3000
API_BASE_URL=http://localhost:3000

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/dukaan_ai
REDIS_URL=redis://localhost:6379

# Authentication
JWT_SECRET=your-secret-key
JWT_EXPIRY=24h

# Marketplace APIs
AMAZON_CLIENT_ID=your-amazon-client-id
AMAZON_CLIENT_SECRET=your-amazon-client-secret
EBAY_CLIENT_ID=your-ebay-client-id
EBAY_CLIENT_SECRET=your-ebay-client-secret
SHOPIFY_API_KEY=your-shopify-api-key
SHOPIFY_API_SECRET=your-shopify-api-secret

# Notifications
SENDGRID_API_KEY=your-sendgrid-key
TWILIO_ACCOUNT_SID=your-twilio-sid
TWILIO_AUTH_TOKEN=your-twilio-token

# Message Queue
RABBITMQ_URL=amqp://localhost:5672
```

### Running Tests

```bash
# Run all tests
npm test

# Run unit tests
npm run test:unit

# Run property-based tests
npm run test:property

# Run integration tests
npm run test:integration

# Generate coverage report
npm run test:coverage
```

## 📚 Documentation

Comprehensive documentation is available in the `.kiro/specs/dukaan-ai/` directory:

- **[Requirements Document](/.kiro/specs/dukaan-ai/requirements.md)**: Detailed functional requirements with 15 core requirements and acceptance criteria
- **[Design Document](/.kiro/specs/dukaan-ai/design.md)**: System architecture, component interfaces, and 51 correctness properties
- **[API Documentation](docs/api.md)**: RESTful API endpoints and usage examples *(coming soon)*
- **[Integration Guide](docs/integrations.md)**: Marketplace API integration instructions *(coming soon)*
- **[Deployment Guide](docs/deployment.md)**: Production deployment and scaling strategies *(coming soon)*

### Key Documents

#### Requirements Highlights

The platform addresses 15 core requirements across:
1. Competitive Price Monitoring
2. Price Change Tracking and Analysis
3. Dynamic Pricing Recommendations
4. Price Elasticity Analysis
5. Demand Forecasting
6. Inventory Optimization
7. Analytics Dashboard
8. Actionable Insights and Alerts
9. Marketplace API Integration
10. Automated Price Updates
11. Reporting and Export
12. Webhook Notifications
13. Multi-User Access and Permissions
14. Data Security and Privacy
15. System Performance and Scalability

#### Design Highlights

The design document includes:
- Microservices architecture with 6 core services
- 51 correctness properties for property-based testing
- Comprehensive error handling strategies
- Dual testing approach (unit + property-based)
- Security and compliance considerations

## 🗺 Roadmap

### Phase 1: MVP (Q2 2026)
- [x] Requirements and design documentation
- [ ] Core price monitoring service
- [ ] Basic pricing engine with competitive strategy
- [ ] Simple analytics dashboard
- [ ] Amazon marketplace integration

### Phase 2: Enhanced Intelligence (Q3 2026)
- [ ] Demand forecasting engine
- [ ] Inventory optimization
- [ ] Price elasticity analysis
- [ ] eBay and Shopify integrations
- [ ] Alert system with email notifications

### Phase 3: Advanced Features (Q4 2026)
- [ ] Premium and clearance pricing strategies
- [ ] Webhook support
- [ ] Advanced reporting and exports
- [ ] Mobile-responsive dashboard
- [ ] Multi-user access control

### Phase 4: Enterprise Scale (Q1 2027)
- [ ] Machine learning model improvements
- [ ] Real-time streaming analytics
- [ ] Advanced forecasting (seasonality, events)
- [ ] API rate optimization
- [ ] White-label capabilities

### Future Enhancements
- Multi-currency support
- International marketplace expansion
- Predictive competitor analysis
- Automated repricing bots
- Integration marketplace (Zapier, Make)
- Mobile native apps (iOS, Android)

## 🤝 Contributing

We welcome contributions from the community! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting pull requests.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Standards

- Follow TypeScript best practices
- Write unit tests for all new features
- Write property-based tests for core logic
- Maintain 80%+ code coverage
- Use ESLint and Prettier for code formatting
- Document all public APIs

### Testing Requirements

All contributions must include:
- Unit tests for specific scenarios
- Property-based tests for universal properties
- Integration tests for API endpoints
- Documentation updates

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built for the [AI for Bharat Hackathon](https://dukaanai.nxtgensec.org)
- Inspired by the challenges faced by small marketplace sellers
- Powered by open-source technologies and community contributions

## 📞 Contact & Support

- **Project Lead**: [Your Name](mailto:kiransavireddy@gmail.com@example.com)
- **Documentation**: [docs.dukaan-ai.com](https://docs.dukaan-ai.com) *(coming soon)*
- **Issue Tracker**: [GitHub Issues](https://github.com/SavireddyKiranKumarReddy/dukaan-ai/issues)
- **Community**: [Discord Server](https://discord.gg/dukaan-ai) *(coming soon)*

## 🌟 Star History

If you find Dukaan AI useful, please consider giving it a star ⭐ on GitHub!

---

**Built with ❤️ for marketplace sellers worldwide**

*Empowering small businesses with enterprise-grade pricing intelligence*
