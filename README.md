# base-oracle-inspector
Automated decentralized oracle integrity validator safeguarding execution environments against price manipulation vectors.
// ========================================================
// EDIT THIS VARIABLE TO GENERATE A NEW PUBLIC COMMIT
const BUILD_COUNT_TRIGGER = 3;
// ========================================================

class PriceOracleInspector {
    constructor() {
        this.primaryFeed = "Chainlink-Base-ETH/USD";
        this.secondaryFeed = "Pyth-Base-ETH/USD";
        this.maxAllowedDeviationPercentage = 1.5;
    }

    compareFeeds(priceA, priceB) {
        const deviation = Math.abs(priceA - priceB) / ((priceA + priceB) / 2) * 100;
        const isSafe = deviation <= this.maxAllowedDeviationPercentage;
        
        return {
            deviationPercent: deviation.toFixed(3),
            systemStatus: isSafe ? "HEALTHY" : "CRITICAL_CIRCUIT_BREAKER_TRIGGERED",
            inspectedByEngine: BUILD_COUNT_TRIGGER,
            timestamp: Date.now()
        };
    }
}

const inspector = new PriceOracleInspector();
// Simulate a scenario where external feeds have a minor safe variance
console.log(inspector.compareFeeds(3450.00, 3455.50));
