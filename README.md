# Real-Time Financial Trading System

## 📖 Description

This project is a high-performance financial trading system that simulates real-world stock market operations using advanced software engineering patterns and data structures. Built with Java 17, the system demonstrates how modern trading platforms handle thousands of transactions per second while maintaining data integrity and enabling lightning-fast queries.

At its core, the system implements **Event Sourcing**, an architectural pattern where all changes to application state are stored as a sequence of immutable events. This approach provides a complete audit trail of every trade and price update, enabling compliance reporting, debugging, and the ability to replay historical data for analysis. Unlike traditional CRUD systems that overwrite data, event sourcing preserves the entire history, making it ideal for financial applications where regulatory requirements demand perfect record-keeping.

The system leverages **B-Tree indexing** through Java's TreeMap data structure to achieve O(log n) search performance. Multiple indexes are maintained simultaneously—organizing trades by stock symbol, trader name, transaction amount, and timestamp. This multi-index strategy allows different services to query the same data efficiently from different perspectives. For example, the Portfolio Analytics Service can instantly retrieve all trades for a specific trader, while the Risk Management Service can quickly identify transactions exceeding certain thresholds.

Four independent microservices demonstrate real-world financial operations: **Trade Execution** processes buy/sell orders, **Price Monitoring** detects market volatility and price spikes, **Risk Management** identifies suspicious trading patterns and anomalies, and **Portfolio Analytics** generates comprehensive reports showing each trader's positions and profit/loss.

The architecture showcases decoupled design where services operate independently, querying the central event store without sharing mutable state. This separation enables easy scaling, testing, and maintenance—critical requirements for production financial systems. The implementation serves as an educational resource for understanding how high-frequency trading platforms achieve both performance and reliability in mission-critical environments.

## 🎯 Features

- **Event Store**: Immutable event log storing all trading and price events
- **B-Tree Indexes**: O(log n) search performance with range queries
- **Real-Time Processing**: Multiple services process events independently
- **Trade Execution**: Buy/sell order processing with automatic indexing
- **Price Monitoring**: Volatility detection and price spike alerts
- **Risk Management**: Anomaly detection in trading patterns
- **Portfolio Analytics**: Per-trader position and P&L reports

## 🏗️ Architecture

```
┌─────────────────┐
│   Event Store   │  ← Immutable event log (source of truth)
└────────┬────────┘
         │
    ┌────┴────┐
    │ B-Tree  │  ← Multiple indexes for fast queries
    │ Index   │     - By Symbol
    └────┬────┘     - By Trader
         │          - By Amount
    ┌────┴──────────────────┐
    │   Service Layer       │
    ├───────────────────────┤
    │ • Trade Execution     │
    │ • Price Monitoring    │
    │ • Risk Management     │
    │ • Portfolio Analytics │
    └───────────────────────┘
```

## 📁 Project Structure

```
src/
├── main/
│   └── java/
│       └── com/stocks/
│           ├── Main.java                    # Application entry point
│           ├── domain/
│           │   ├── Alert.java               # Alert notifications
│           │   ├── StockPrice.java          # Price event model
│           │   └── TradeEvent.java          # Trade event model
│           ├── service/
│           │   ├── PortfolioAnalyticsService.java   # Portfolio reports
│           │   ├── PriceMonitoringService.java      # Price analysis
│           │   ├── RiskManagementService.java       # Risk detection
│           │   └── TradeExecutionService.java       # Trade processing
│           └── store/
│               ├── BTreeIndex.java          # In-memory B-Tree indexes
│               └── EventStore.java          # Event storage & replay
└── test/
    └── java/
```

## 🚀 Quick Start

### Prerequisites

- Java 17 or higher
- Maven (optional, can use javac)

### Option 1: Using javac

**Compile:**
```bash
javac -d bin src/main/java/com/stocks/domain/*.java src/main/java/com/stocks/store/*.java src/main/java/com/stocks/service/*.java src/main/java/com/stocks/Main.java
```

**Run:**
```bash
java -cp bin com.stocks.Main
```

### Option 2: Using Maven

**Compile:**
```bash
mvn compile
```

**Run:**
```bash
mvn exec:java -Dexec.mainClass="com.stocks.Main"
```

**Or combined:**
```bash
mvn compile exec:java -Dexec.mainClass="com.stocks.Main"
```

## 📊 Sample Output

```
╔════════════════════════════════════════════════════════════╗
║   REAL-TIME FINANCIAL TRADING SYSTEM                       ║
║   Event Streams + B-Tree Indexes for High Performance      ║
╚════════════════════════════════════════════════════════════╝

┌─────────────────────────────────────────────────────┐
│ 📡 PHASE 1: LIVE MARKET PRICES                      │
└─────────────────────────────────────────────────────┘
✓ Recorded 20 price events

┌─────────────────────────────────────────────────────┐
│ 💹 PHASE 2: TRADE EXECUTION                         │
└─────────────────────────────────────────────────────┘
📌 EXECUTING: TradeEvent[trader=Alice, symbol=AAPL, ...]

╔════════════════════════════════════════════════════════════╗
║        QUERYING DATA WITH B-TREE INDEXES                   ║
╚════════════════════════════════════════════════════════════╝

🔍 Searching trades for: AAPL
  ⏱️  Time: 2ms (B-Tree O(log n))
  📊 Found: 5 trades
```

## 🔍 Key Concepts

### Event Sourcing
All state changes are stored as immutable events in the Event Store, providing:
- Complete audit trail
- Time-travel debugging
- Easy service replay
- Compliance-ready logging

### B-Tree Indexing
Multiple TreeMap-based indexes enable:
- **O(log n)** single key lookups
- **O(log n + k)** range queries (k = result count)
- Sorted iteration
- Efficient memory usage

### Service Independence
Each service independently queries the Event Store:
- No shared mutable state
- Easy to add new services
- Service-specific views of data

## 📈 Performance

- **Trade Execution**: < 5ms per trade
- **Index Queries**: O(log n) time complexity
- **Range Queries**: O(log n + k) where k is result size
- **Event Store**: Append-only for maximum write throughput

## 🔧 Configuration

Edit `Main.java` to customize:
- Number of simulated trades
- Stock symbols
- Trader names
- Query parameters

## 🧪 Testing

The main method includes built-in demonstrations:
1. 20 random price events
2. 25 random trade executions
3. Multiple query scenarios
4. Portfolio reports for sample traders

## 📚 Tech Stack

- **Java 17**: Records, text blocks, streams
- **TreeMap**: Red-black tree implementation (B-Tree-like)
- **Streams API**: Functional data processing
- **Event-Driven**: Decoupled architecture

## 🎓 Learning Objectives

This project demonstrates:
- Event sourcing patterns
- B-Tree data structure usage
- Real-time data processing
- Financial system design
- Time complexity optimization

## 📝 License

This is a learning/demonstration project.

## 👤 Author

Created for educational purposes to demonstrate high-performance financial data processing.

---

**Note**: This is an in-memory implementation. Production systems would use persistent storage (databases) and distributed architectures.
