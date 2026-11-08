# PressVote — Campus poster ballot

MG3012 · Assignment 2 · Blockchain Technology for Business

Students choose which poster should advertise a campus makers’ fair. Each Ethereum address gets one vote per deployment. Anyone can read the two totals. The interface turns the totals into percentage bars and links each submitted transaction to its Sepolia receipt.

**Network:** Ethereum Sepolia (chain ID 11155111)  
**Contract address:** [0xF02e79041daCbA6a2D929607326752869a005B9a](https://sepolia.etherscan.io/address/0xF02e79041daCbA6a2D929607326752869a005B9a)  
**Public GitHub repository:** [MG3012-PressVote](https://github.com/ahmedaslamuk-coder/MG3012-PressVote)

The voting page already contains the address above. To use this deployment, start with section 2. Screenshot 1 is included.


## How the contract and page work

| Solidity function | Kind | What it does |
| --- | --- | --- |
| castVote(uint8 option) | Write | Accepts 0 for Night Market or 1 for Fresh Type. Rejects other IDs and repeat votes from the same sender. Marks the sender as having voted, increments one counter and emits VoteCast. |
| getResults() | Read | Returns both counters in option order. |
| hasVoted(address voter) | Read | Looks up whether the given wallet has cast a vote. |

The HTML includes the function signatures (the ABI) so ethers.js can encode each call. MetaMask supplies the selected account. The signer authorizes a write and pays testnet gas. The page waits for the transaction receipt before reporting success. The contract enforces the one-vote rule even if someone bypasses the page. A person who controls two addresses can vote once from each. Vote choices are public in the transaction and event.

**Bonus UI feature:** Each result bar displays the option’s share of confirmed votes. For example, two Night Market votes and one Fresh Type vote display as 66.6% and 33.3% (truncated to one decimal). With zero votes both bars start empty.

## Capture evidence and submit

Included screenshots:

- [Sepolia deployment](screenshots/01-deployment.png)
- [Local Remix VM deployment](screenshots/remix-vm.png)
- [Wallet setup alongside the Remix VM](screenshots/wallet-setup.png)
- [Remix connected to MetaMask](screenshots/remix-wallet-connected.png)
- [Sepolia faucet transfer completed](screenshots/faucet.png)
- [MetaMask deployment request on Sepolia](screenshots/deployment-request.png)
- [Remix reads the initial vote totals (0, 0)](screenshots/initial-results.png)
- [Voting page with Fresh Type selected and wallet disconnected](screenshots/ballot-preview.png)

To complete the frontend evidence, capture the connected ballot and a confirmed vote with the updated totals and transaction hash.

Submit the project ZIP, public repository URL and Sepolia contract address in Google Classroom.

## Troubleshooting

- **No contract found:** Compare the address with the deployed contract in Remix. Verify the selected chain is Sepolia. A wallet address or a Remix VM deployment will not work here.
- **Wallet request cancelled:** Click the button again when ready. A cancelled signature does not use a vote.
- **Insufficient funds:** Add Sepolia test ETH to the account selected in MetaMask, then retry.
- **Wallet already voted:** The original count remains. To demonstrate a first vote again, use another funded test account.
- **Confirmation is slow:** Follow the displayed transaction hash to inspect its status before retrying.

References: [Remix deployment documentation](https://remix-ide.readthedocs.io/en/latest/run.html) · [ethers.js guide](https://docs.ethers.org/v6/getting-started/)
