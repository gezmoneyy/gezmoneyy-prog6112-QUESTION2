const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

class IConsoles {
    getConsoleType() {
        throw new Error("getConsoleType() must be implemented");
    }
    
    getStore() {
        throw new Error("getStore() must be implemented");
    }
    
    getTotalSales() {
        throw new Error("getTotalSales() must be implemented");
    }
}

class Consoles extends IConsoles {
    constructor(consoleType, storeName, totalSales) {
        super();
        this.consoleType = consoleType;
        this.storeName = storeName;
        this.totalSales = totalSales;
    }

    getConsoleType() {
        return this.consoleType;
    }

    getStore() {
        return this.storeName;
    }

    getTotalSales() {
        return this.totalSales;
    }
}

class ConsoleSales extends Consoles {
    constructor(consoleType, storeName, totalSales) {
        super(consoleType, storeName, totalSales);
    }

    printReport() {
        console.log("\nCONSOLE SALES REPORT");
        console.log("********************");
        console.log(`CONSOLE TYPE: ${this.getConsoleType()}`);
        console.log(`STORE: ${this.getStore()}`);
        console.log(`TOTAL SALES: ${this.getTotalSales()}`);
    }
}

function runApplication() {
    console.log("Select the console type");
    console.log("1) PS5");
    console.log("2) XBOX");
    console.log("3) SWITCH\n");

    rl.question("", (choice) => {
        const consoles = {
            '1': 'PS5',
            '2': 'XBOX',
            '3': 'SWITCH'
        };
        
        const selectedConsole = consoles[choice];

        rl.question("Enter the store: ", (storeName) => {
            rl.question(`Enter the total sales of ${selectedConsole} consoles for ${storeName}:`, (salesInput) => {
                const totalSales = parseInt(salesInput);

                const salesReport = new ConsoleSales(
                    selectedConsole,
                    storeName,
                    totalSales
                );

                salesReport.printReport();
                rl.close();
            });
        });
    });
}

runApplication();
