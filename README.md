# IE Tech Venture Bootcamp October 2024 - XRP Ledger

## Overview
This repository, created by Professor Manoel Gadi, is for the IE Tech Venture Bootcamp October 2024 edition. It focuses on the XRP Ledger, a public decentralized blockchain backed by Ripple Labs.

## Definition of XRP Ledger
Launched in June 2012, the XRP Ledger is a public decentralized blockchain that enables fast, real-time, and low-cost transactions. It is environmentally friendly due to its low energy consumption, achieved through the Ripple Protocol Consensus Algorithm (RPCA) instead of Proof of Work or Proof of Stake. The platform supports payments, tokenization, NFTs, and DeFi (Decentralized Finance) and is open to everyone. The native cryptocurrency is XRP.

## Ripple Protocol Consensus Algorithm
The RPCA uses a network of independent validators to confirm transactions every 3 to 5 seconds. Unlike Proof of Work, where miners solve mathematical problems for rewards, RPCA validators quickly approve or disapprove transactions. Over 120 validators, operated by universities, companies, and individuals, ensure the blockchain's decentralization.

## Hooks
Hooks are code snippets that allow developers to customize or add tasks or conditions directly in the XRP Ledger. Written in any language and compiled with WebAssembly, hooks provide flexibility and customization in development. For example, a hook can notify you each time a transaction occurs between accounts.

## Key Concepts

### Escrow
Escrow is a security mechanism where XRP amounts are blocked until contract terms are fulfilled. It involves a third party holding assets until conditions are met. Escrow can be based on:
- **Time**: Funds are released after a set period.
- **Conditions**: Funds are released when specific conditions are met.
- **Combination**: A mix of time and conditions.

### Oracle
Oracles are third-party participants that provide blockchains with real-world information, such as currency prices or stock exchange data, to validate smart contracts. An oracle can be an entity or software, like an IoT device that confirms merchandise delivery to trigger payment.

## Installation
To install the necessary packages, run:
```bash
pip install xrpl-py
```

## Example Usage
```python
import nest_asyncio
nest_asyncio.apply()
from xrpl.account import get_balance
from xrpl.clients import JsonRpcClient
from xrpl.models import Payment, Tx
from xrpl.transaction import submit_and_wait
from xrpl.wallet import generate_faucet_wallet

# Create a client to connect to the test network
client = JsonRpcClient("https://s.altnet.rippletest.net:51234")

# Create two wallets to send money between on the test network
wallet1 = generate_faucet_wallet(client, debug=True)
wallet2 = generate_faucet_wallet(client, debug=True)

# Check balances before transaction
print("Balances of wallets before Payment tx")
print("Wallet 1 balance:", get_balance(wallet1.address, client))
print("Wallet 2 balance:", get_balance(wallet2.address, client))

# Create a Payment transaction from wallet1 to wallet2
payment_tx = Payment(
    account=wallet1.address,
    amount="12345",
    destination=wallet2.address,
)

# Submit the payment to the network and wait for a response
payment_response = submit_and_wait(payment_tx, client, wallet1)
print("Transaction was submitted")

# Check whether the transaction was validated on the ledger
tx_response = client.request(Tx(transaction=payment_response.result["hash"]))
print("Validated:", tx_response.result["validated"])

# Check balances after transaction
print("Balances of wallets after Payment tx:")
print(get_balance(wallet1.address, client))
print(get_balance(wallet2.address, client))
```

## Further References
- [XRPL-Commons](https://github.com/XRPL-Commons/IE-Tech-Venture-Bootcamp-2024)
- [XRP.org](https://xrpl.org/)

Source: Conversation with Copilot, 5/10/2024
(1) XRPL-Commons/IE-Tech-Venture-Bootcamp-2024 - GitHub. https://github.com/XRPL-Commons/IE-Tech-Venture-Bootcamp-2024.
(2) 2024-XRP-Repository/README.md at master - GitHub. https://github.com/FRC1732/2024-XRP-Repository/blob/master/README.md.
(3) Client Libraries - XRPL. https://xrpl.org/docs/references/client-libraries.
(4) undefined. https://github.com/XRPL-Commons/community-ideas/blob/main/hackathon/index.md.
(5) undefined. https://www.youtube.com/channel/UCwlHiotQWku7DztcnH3zrzw.
(6) undefined. https://docs.xrpl-commons.org.
(7) undefined. https://xrpl.org.
(8) undefined. https://learn.xrpl.org.
(9) undefined. https://github.com/XRPL-Commons/xrpl-commons-tutorials.
(10) undefined. https://github.com/XRPL-Commons/Jan2024_EVM_Links.
(11) undefined. https://github.com/XRPL-Commons/Jan2024_web3/blob/main/readme.md.
(12) undefined. https://github.com/XRPL-Commons/xrpl-training-april-2024.
