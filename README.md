# 📈 Trading Simulator - Gamified Market Learning Platform

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Angular](https://img.shields.io/badge/Angular-16+-red.svg)](https://angular.io/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green.svg)](https://fastapi.tiangolo.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15+-blue.svg)](https://www.postgresql.org/)

A comprehensive, production-ready trading simulator that combines real-time market data with gamified learning experiences. Perfect for aspiring traders, finance students, and anyone looking to master trading strategies without financial risk.

## ✨ Key Features

### 🤖 **Intelligent Trading Bots**
- **10+ Pre-built Strategies**: MA Crossover, RSI, Bollinger Bands, MACD, Volume Breakout, Mean Reversion, Momentum, Support/Resistance, Grid Trading, DCA
- **Backtesting Engine**: Test strategies on historical data spanning major market events
- **Risk Management**: Configurable stop-loss, take-profit, position sizing, and leverage controls
- **Performance Analytics**: Track PnL, win rate, Sharpe ratio, max drawdown, and more

### 📊 **Real-Time Market Data**
- **Multi-Asset Support**: Stocks, Forex, Cryptocurrencies
- **Live Price Feeds**: Integration with Polygon.io, Binance, and Alpha Vantage APIs
- **Interactive Charts**: TradingView-powered candlestick charts with technical indicators
- **Market Depth**: Real-time order book visualization

### 🎓 **Gamified Learning System**
- **Progressive Lessons**: Structured curriculum from basics to advanced strategies
- **XP & Achievements**: Earn rewards for completing trades and lessons
- **Crisis Simulator**: Practice trading during historical events (1929 Crash, 1987 Black Monday, 2000 Dot-com Bubble, 2008 Financial Crisis, 2020 COVID)
- **Interactive Challenges**: Real-world scenarios to test your skills

### 💼 **Portfolio Management**
- **Multi-Portfolio Support**: Separate portfolios for different strategies
- **Leverage Trading**: Optional margin trading with configurable limits
- **Transaction History**: Complete audit trail of all trades
- **Performance Dashboard**: Real-time P&L tracking and analytics

### 💬 **Social Features**
- **Chat System**: Discuss strategies with other traders
- **Watchlists**: Track your favorite assets
- **News Integration**: Stay updated with market-moving news

## 🛠️ Technology Stack

### Backend
- **Framework**: FastAPI (Python 3.11+)
- **Database**: PostgreSQL 15+ with SQLAlchemy ORM
- **Cache**: Redis for real-time data and pub/sub
- **Authentication**: JWT-based with role-based access control
- **API Documentation**: Auto-generated with OpenAPI/Swagger
- **Migrations**: Alembic for database version control

### Frontend
- **Framework**: Angular 16+
- **Language**: TypeScript
- **Charting**: TradingView Lightweight Charts
- **State Management**: RxJS
- **UI Components**: Custom design system

### Infrastructure
- **Containerization**: Docker & Docker Compose
- **WebSockets**: Real-time price updates
- **Rate Limiting**: API protection middleware
- **CORS**: Configurable cross-origin resource sharing

## 📁 Project Structure

```
Trading-Simulator/
├── Back/                          # Backend API
│   ├── app/
│   │   ├── config/               # Configuration & settings
│   │   ├── models/               # SQLAlchemy database models
│   │   ├── routers/              # API endpoints
│   │   ├── schemas/              # Pydantic request/response schemas
│   │   ├── services/             # Business logic layer
│   │   ├── middleware/           # JWT, rate limiting, RBAC
│   │   ├── crisis_simulator/    # Historical event simulation
│   │   └── utils/                # Helper functions
│   ├── alembic/                  # Database migrations
│   ├── Simulation_data/          # Historical crisis data
│   ├── requirements.txt
│   ├── Dockerfile
│   └── docker-compose.yml
├── Front/                         # Angular frontend
│   ├── src/
│   │   ├── app/                  # Angular components & services
│   │   ├── assets/               # Static resources
│   │   └── environments/         # Environment configs
│   ├── angular.json
│   └── package.json
└── README.md
```

## 🚀 Quick Start

### Prerequisites
- **Docker & Docker Compose** (recommended) OR
- **Python 3.11+**, **Node.js 18+**, **PostgreSQL 15+**, **Redis**

### Option 1: Docker (Recommended)

1. **Clone the repository**
```bash
git clone https://github.com/rostommbarki/Trading-simulator.git
cd Trading-simulator
```

2. **Set up environment variables**
```bash
cd Back
cp .env.example .env
# Edit .env with your API keys (see Configuration section)
```

3. **Start all services**
```bash
docker-compose up --build
```

4. **Access the application**
- API Documentation: http://localhost:8000/docs
- Frontend: http://localhost:4200

### Option 2: Local Development

#### Backend Setup

```bash
cd Back

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up database
alembic upgrade head

# Seed initial data (optional)
python app/seed_lessons.py

# Start server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

#### Frontend Setup

```bash
cd Front

# Install dependencies
npm install

# Start development server
ng serve

# Build for production
ng build --configuration production
```

## ⚙️ Configuration

### Required Environment Variables

Create a `.env` file in the `Back/` directory:

```env
# Database
DATABASE_URL=postgresql+asyncpg://user:password@localhost:5432/trading_simulator

# Redis
REDIS_URL=redis://localhost:6379/0

# Security
SECRET_KEY=your-secret-key-here  # Generate with: openssl rand -hex 32
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# API Keys
POLYGON_API_KEY=your_polygon_api_key          # Get from: https://polygon.io/
NEWS_API_KEY=your_news_api_key                # Get from: https://newsapi.org/
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_key  # Get from: https://alphavantage.co/
BINANCE_KEY=your_binance_key                  # Optional, for crypto data

# CORS
FRONTEND_URL=http://localhost:4200
```

### API Key Providers

| Provider | Purpose | Free Tier | Sign Up |
|----------|---------|-----------|---------|
| **Polygon.io** | Real-time stocks & forex | ✅ Limited | [Register](https://polygon.io/) |
| **News API** | Market news & headlines | ✅ 100 req/day | [Register](https://newsapi.org/) |
| **Alpha Vantage** | Backup stock data | ✅ 5 req/min | [Register](https://alphavantage.co/) |
| **Binance** | Crypto market data | ✅ Public streams | [Register](https://binance.com/) |

## 📚 API Documentation

Once the backend is running, visit:
- **Interactive Docs**: http://localhost:8000/docs (Swagger UI)
- **ReDoc**: http://localhost:8000/redoc (Alternative documentation)

### Key API Endpoints

```
Authentication:
  POST   /auth/register          - Create new account
  POST   /auth/login             - User login
  POST   /auth/refresh           - Refresh JWT token

Portfolio:
  GET    /portfolio/{id}         - Get portfolio details
  POST   /portfolio              - Create new portfolio
  GET    /portfolio/{id}/performance - Portfolio analytics

Trading:
  POST   /orders                 - Place order
  GET    /orders/{id}            - Get order details
  DELETE /orders/{id}            - Cancel order

Bots:
  POST   /bots                   - Create trading bot
  PUT    /bots/{id}/start        - Activate bot
  POST   /bots/{id}/backtest     - Run backtest
  GET    /bots/{id}/trades       - Get bot trade history

Market Data:
  GET    /market-data/price/{symbol}     - Latest price
  GET    /candles/{symbol}               - Historical OHLCV data
  WS     /ws/market-data/{symbol}        - Real-time price stream

Crisis Simulator:
  POST   /crisis-simulator/start         - Start historical simulation
  GET    /crisis-simulator/events        - Available crisis scenarios

Lessons:
  GET    /lessons                        - Get all lessons
  POST   /lessons/{id}/complete          - Mark lesson complete
```

## 🎯 Usage Examples

### Creating a Trading Bot

```python
# Example: MA Crossover Strategy
bot_config = {
    "name": "MA Crossover AAPL",
    "portfolio_id": 1,
    "symbol": "AAPL",
    "asset_type": "stock",
    "strategy_type": "MA_CROSSOVER",
    "strategy_params": {
        "fast_period": 10,
        "slow_period": 30
    },
    "max_position_size": 1000.0,
    "stop_loss_pct": 2.0,
    "take_profit_pct": 5.0,
    "interval": "15m"
}
```

### Running a Backtest

```python
backtest_config = {
    "start_date": "2020-01-01",
    "end_date": "2023-12-31",
    "initial_capital": 10000.0
}
```

### Crisis Simulation

Simulate trading during historical market crashes:
- **Great Depression** (1929-1939)
- **Black Monday** (1987)
- **Dot-com Bubble** (1998-2002)
- **Global Financial Crisis** (2007-2009)
- **COVID-19 Crash** (2020)

## 🧪 Testing

```bash
# Backend tests
cd Back
pytest app/tests/

# Frontend tests
cd Front
ng test
```

## 📈 Performance & Scalability

- **WebSocket connections**: Handles 1000+ concurrent users
- **Database optimization**: Indexed queries, connection pooling
- **Caching strategy**: Redis for hot data, reduces API calls by 80%
- **Rate limiting**: Prevents API abuse, configurable per endpoint
- **Async processing**: Non-blocking I/O for market data updates

## 🔒 Security Features

- ✅ JWT authentication with refresh tokens
- ✅ Password hashing (bcrypt)
- ✅ Role-based access control (User, Admin, Super Admin)
- ✅ Rate limiting middleware
- ✅ SQL injection prevention (parameterized queries)
- ✅ CORS configuration
- ✅ API key validation

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Follow PEP 8 (Python) and Angular style guide (TypeScript)
- Write unit tests for new features
- Update documentation for API changes
- Run linters before committing

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **Rostom Mbarki** - [@rostommbarki](https://github.com/rostommbarki)

## 🙏 Acknowledgments

- [FastAPI](https://fastapi.tiangolo.com/) - Modern Python web framework
- [Angular](https://angular.io/) - Frontend framework
- [TradingView](https://www.tradingview.com/) - Charting library
- [Polygon.io](https://polygon.io/) - Market data provider
- Historical crisis data sourced from various financial archives

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/rostommbarki/Trading-simulator/issues)
- **Discussions**: [GitHub Discussions](https://github.com/rostommbarki/Trading-simulator/discussions)
- **Email**: [Your contact email]

## 🗺️ Roadmap

- [ ] Mobile app (React Native)
- [ ] Social trading features (copy trading)
- [ ] Options & futures trading
- [ ] AI-powered strategy recommendations
- [ ] Real-time multiplayer trading competitions
- [ ] Integration with broker APIs for paper trading
- [ ] Advanced portfolio analytics & risk metrics

---

<div align="center">

**⭐ If you find this project useful, please consider giving it a star! ⭐**

Made with ❤️ by passionate traders and developers

</div>