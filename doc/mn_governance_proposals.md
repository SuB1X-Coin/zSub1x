## SUB1X Governance powered by the blockchain

The SUB1X Community Governance will allow anyone with a SUB1X wallet to submit project proposals for new exchanges, marketing, dev, integrations, etc and get the requested SUB1X coins if MasterNode owners vote it **Yes**

### Create a proposal

All the commands assume a CLI wallet. You can run them in the debug console of a Qt wallet as well, just remove the `$ zsub1x-cli ` part from the commands.

### Identify the next budget superblock to pin the proposal to

```
$ zsub1x-cli getnextsuperblock
144
```

### Create an address in the wallet that will receive the funds if the proposal is voted Yes by the MasterNodes:
```
$ zsub1x-cli getaccountaddress "proposal1"
yKdGJkWJm4fXTrRmpvrXjpL4r8eMnnBeLd
```

### Create the proposal using the superblock and address from above. In this example we are asking for 20 SUB1X coins. Min amount that can be requested is `0.04`
### The URL is there to provide additional details about the proposal so that MN owners can decide if they should vote it yes or no
```
$ zsub1x-cli preparebudget "test1" "http://example.com/proposal1" 1 144 "yKdGJkWJm4fXTrRmpvrXjpL4r8eMnnBeLd" 20
2e21cae5c69209d648734653e3dcca85c67ac96e08a48d99923de58e9ba222d3
```

### Wait for the 0.04 SUB1X proposal fee transaction to gain 6 confirmations
```
$ zsub1x-cli gettransaction 2e21cae5c69209d648734653e3dcca85c67ac96e08a48d99923de58e9ba222d3
```

### Once we have 6 confirmations for the proposal fee, we can submit the proposal
```
$ zsub1x-cli submitbudget "test1" "http://example.com/proposal1" 1 144 "yKdGJkWJm4fXTrRmpvrXjpL4r8eMnnBeLd" 20 "2e21cae5c69209d648734653e3dcca85c67ac96e08a48d99923de58e9ba222d3"
```

### See all proposals for this budget cycle
```json
$ zsub1x-cli getbudgetinfo
[
    {
        "Name" : "test1",
        "URL" : "http://example.com/proposal1",
        "Hash" : "1c4c744a3b684b535b0eafe30a9c366e189554a53e9c76b542b9cbba8887f886",
        "FeeHash" : "2e21cae5c69209d648734653e3dcca85c67ac96e08a48d99923de58e9ba222d3",
        "BlockStart" : 144,
        "BlockEnd" : 289,
        "TotalPaymentCount" : 1,
        "RemainingPaymentCount" : 1,
        "PaymentAddress" : "yKdGJkWJm4fXTrRmpvrXjpL4r8eMnnBeLd",
        "Ratio" : 0.00000000,
        "Yeas" : 0,
        "Nays" : 0,
        "Abstains" : 0,
        "TotalPayment" : 20.00000000,
        "MonthlyPayment" : 20.00000000,
        "IsEstablished" : true,
        "IsValid" : true,
        "IsValidReason" : "",
        "fValid" : true
    }
]
```

### Vote yes on the above proposal from the masternode CLI
```
$ zsub1x-cli mnbudgetvote local "1c4c744a3b684b535b0eafe30a9c366e189554a53e9c76b542b9cbba8887f886" yes
```

### Alternatively you can vote from the Cold wallet as well on behalf of multiple masternodes
```
$ zsub1x-cli mnbudgetvote many "1c4c744a3b684b535b0eafe30a9c366e189554a53e9c76b542b9cbba8887f886" yes
```

