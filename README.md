# TrustScan AI

Product Transparency & Lifecycle Intelligence Platform for the AI for Bharat Hackathon.

## Overview

TrustScan AI is a comprehensive platform that addresses critical information asymmetry in retail markets through AI-powered verification, intelligent inventory management, and market intelligence. The system serves three primary user groups:

- **Customers**: Instant product verification through QR scanning or visual recognition
- **Store Owners**: Automated stock verification, expiry management, and AI-powered retail guidance
- **Manufacturers**: Supply chain transparency, grey market detection, and instant recall management

## Architecture

This is a monorepo built with:

- **Backend**: AWS Lambda (Node.js 20.x with TypeScript)
- **Infrastructure**: AWS CDK
- **Database**: Amazon DynamoDB with GSIs
- **Storage**: Amazon S3 with CloudFront CDN
- **Cache**: Amazon ElastiCache (Redis)
- **AI/ML**: AWS Bedrock, Rekognition, SageMaker
- **Events**: Amazon EventBridge
- **Notifications**: Amazon SNS
- **API**: Amazon API Gateway (REST + WebSocket)
- **Build Tool**: Turbo (monorepo orchestration)
- **Testing**: Jest + fast-check (property-based testing)

## Project Structure

```
trustscan-ai/
├── infrastructure/          # AWS CDK infrastructure code
│   ├── bin/                # CDK app entry point
│   ├── lib/                # CDK stacks and constructs
│   │   ├── constructs/     # Reusable CDK constructs
│   │   └── trustscan-ai-stack.ts
│   └── cdk.json
├── services/               # Lambda microservices
│   ├── scan-service/       # Product scanning and QR decoding
│   ├── verification-service/ # Authenticity verification
│   ├── trust-score-service/ # Trust score calculation
│   ├── alert-service/      # Real-time alerts and notifications
│   ├── market-intel-service/ # Market intelligence and trends
│   ├── forecast-service/   # Demand forecasting
│   ├── pricing-service/    # Dynamic pricing
│   └── copilot-service/    # AI Copilot for retail operations
├── packages/               # Shared packages (to be added)
│   ├── types/              # Shared TypeScript types
│   └── utils/              # Shared utilities
├── apps/                   # Frontend applications (to be added)
│   ├── customer-app/       # React Native customer app
│   ├── store-owner-app/    # React Native store owner app
│   └── dashboards/         # React web dashboards
└── .kiro/                  # Kiro spec files
    └── specs/
        └── trustscan-ai/
```

## Prerequisites

- Node.js >= 18.0.0
- npm >= 9.0.0
- AWS CLI configured with appropriate credentials
- AWS CDK CLI: `npm install -g aws-cdk`

## Getting Started

### 1. Install Dependencies

```bash
npm install
```

### 2. Build All Services

```bash
npm run build
```

### 3. Deploy Infrastructure

For development environment:
```bash
npm run deploy:dev
```

For production environment:
```bash
npm run deploy:prod
```

### 4. Run Tests

```bash
# Run all tests
npm test

# Run unit tests only
npm run test:unit

# Run property-based tests only
npm run test:property
```

## AWS Services Configuration

### DynamoDB Tables

- **Products Table**: Stores Product Digital Twin records with GSIs for category trends and serial number lookup
- **Scans Table**: Stores scan records with GSIs for product history, user history, and regional analysis
- **Stores Table**: Stores store profiles with GSI for location-based discovery
- **Inventory Table**: Stores inventory items with GSI for expiry date queries
- **Reviews Table**: Stores product reviews with GSIs for product and user queries
- **Market Data Table**: Stores aggregated market data with GSI for cross-region analysis
- **Demand Forecasts Table**: Stores demand predictions with TTL
- **Recalls Table**: Stores recall notices with GSI for active recalls

### S3 Buckets

- **Images Bucket**: Product images with lifecycle policies (transition to IA after 90 days)
- **Documents Bucket**: Invoices, certificates, labels (transition to Glacier after 180 days)
- **CDN Logs Bucket**: CloudFront access logs

### ElastiCache

- Redis cluster for caching frequently accessed data (trust scores, product info)
- Configured with encryption at rest and in transit
- Multi-AZ for production environment

### API Gateway

- **REST API**: Public endpoints for scanning, verification, market intelligence
- **WebSocket API**: Real-time alerts and notifications for store owners
- Rate limiting: 1000 requests/second with burst of 2000
- API key authentication for external integrations

### Lambda Functions

All Lambda functions are configured with:
- Node.js 20.x runtime
- VPC access for ElastiCache connectivity
- X-Ray tracing enabled
- Appropriate IAM roles with least privilege
- Environment variables for service configuration

## Development Workflow

### Adding a New Service

1. Create service directory: `services/my-service/`
2. Add `src/index.ts` with Lambda handler
3. Add `package.json`, `tsconfig.json`, `jest.config.js`
4. Update `infrastructure/lib/constructs/lambda.ts` to add the Lambda function
5. Update `infrastructure/lib/constructs/api-gateway.ts` to add API routes
6. Build and deploy

### Running Tests

Tests are organized into:
- **Unit tests**: `*.test.ts` - Test specific examples and edge cases
- **Property tests**: `*.property.test.ts` - Test universal properties with fast-check

Example property test:
```typescript
import fc from 'fast-check'

// Feature: trustscan-ai, Property 5: Trust Score Weighted Calculation
describe('Property: Trust Score Weighted Calculation', () => {
  it('should calculate weighted sum correctly for any signal values', () => {
    fc.assert(
      fc.property(
        fc.integer({ min: 0, max: 100 }),
        fc.integer({ min: 0, max: 100 }),
        fc.integer({ min: 0, max: 100 }),
        fc.integer({ min: 0, max: 100 }),
        (auth, tamp, fresh, social) => {
          const expected = auth * 0.30 + tamp * 0.30 + fresh * 0.25 + social * 0.15
          const result = calculateTrustScore({ auth, tamp, fresh, social })
          expect(result.overall).toBeCloseTo(expected, 2)
        }
      ),
      { numRuns: 100 }
    )
  })
})
```

## Environment Variables

Each Lambda service uses the following environment variables (automatically set by CDK):

- `ENVIRONMENT`: dev/prod
- `PRODUCT_TABLE`: DynamoDB products table name
- `SCAN_TABLE`: DynamoDB scans table name
- `STORE_TABLE`: DynamoDB stores table name
- `INVENTORY_TABLE`: DynamoDB inventory table name
- `REVIEW_TABLE`: DynamoDB reviews table name
- `MARKET_DATA_TABLE`: DynamoDB market data table name
- `DEMAND_FORECAST_TABLE`: DynamoDB demand forecasts table name
- `RECALL_TABLE`: DynamoDB recalls table name
- `IMAGES_BUCKET`: S3 images bucket name
- `DOCUMENTS_BUCKET`: S3 documents bucket name
- `REDIS_ENDPOINT`: ElastiCache Redis endpoint
- `EVENT_BUS_NAME`: EventBridge event bus name
- `ALERTS_TOPIC_ARN`: SNS alerts topic ARN
- `RECALLS_TOPIC_ARN`: SNS recalls topic ARN
- `COUNTERFEIT_TOPIC_ARN`: SNS counterfeit topic ARN
- `EXPIRY_TOPIC_ARN`: SNS expiry topic ARN

## Deployment

### CDK Commands

```bash
# Synthesize CloudFormation template
npm run synth

# Show differences between deployed stack and current state
npm run diff

# Deploy all stacks
npm run deploy

# Deploy to specific environment
npm run deploy:dev
npm run deploy:prod
```

### CI/CD

(To be configured in later tasks)

## Monitoring and Logging

- **CloudWatch Logs**: All Lambda functions log to CloudWatch
- **X-Ray Tracing**: Distributed tracing enabled for all services
- **CloudWatch Metrics**: API Gateway, Lambda, DynamoDB metrics
- **VPC Flow Logs**: Network traffic monitoring

## Security

- **Encryption at Rest**: DynamoDB and S3 use AWS-managed encryption
- **Encryption in Transit**: TLS 1.3 for all API communications
- **IAM Roles**: Least privilege access for all Lambda functions
- **VPC**: Lambda functions run in private subnets
- **Security Groups**: Restrict access to ElastiCache
- **API Gateway**: Rate limiting and API key authentication

## Cost Optimization

- **DynamoDB**: Pay-per-request billing mode
- **Lambda**: Serverless with automatic scaling
- **S3**: Lifecycle policies to transition to cheaper storage classes
- **ElastiCache**: Right-sized instances (t4g.micro for dev, r6g.large for prod)
- **CloudFront**: Price class 100 (North America and Europe only)

## Next Steps

See `.kiro/specs/trustscan-ai/tasks.md` for the complete implementation plan.

Current status: **Task 1 Complete** - Infrastructure and AWS services set up

Next tasks:
- Task 2: Implement core data models and database layer
- Task 3: Implement QR Scanner and Visual Recognition components
- Task 4: Implement Trust Score Calculator

## License

Proprietary - AI for Bharat Hackathon Project

## Contact

For questions or issues, please refer to the project documentation in `.kiro/specs/trustscan-ai/`.
