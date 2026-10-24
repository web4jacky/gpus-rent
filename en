# Rent a GPU with crypto: from choosing a card to boot on NovaPod

A low hourly number is an easy way to pick the wrong cloud GPU. The card then runs out of memory, the template does not match the job, or the deposit lands on the wrong chain. NovaPod (https://novapod.io) splits that into steps you can check: choose by VRAM, read the live ask, fund the balance with crypto, and boot from a template. Billing runs per second. When the machine stops, that charge stops.

This article follows the site as it works now. Asks move, so it does not lock in “what an H100 costs today.” For the number, open the price page and the marketplace.

## What the site actually rents

NovaPod is a GPU rental market billed per second. You are renting a machine you can boot, either a Docker pod or a root KVM virtual machine, not a monthly plan. Typical jobs are an OpenAI-compatible server with vLLM, a short LoRA fine-tune, or an image and video batch in ComfyUI.

The hourly figure on a page is an ask, not a contract rate. The marketplace leads with the current lowest ask. A median often sits beside it so you can see whether that low number is far from most offers. You accept that spot offer. A number from an older article is not the rate.

The account balance pays for time the machine is running. The balance comes from a crypto deposit. The site accepts USDT, USDC, SOL, ETH, and BNB across Solana, Ethereum, BNB Smart Chain, and TRON. One stablecoin unit counts as one dollar of credit. SOL, ETH, and BNB have to be converted into a coin quantity before you send them.

## Ask about VRAM before you ask about price

Pick the card in that order. First ask how much memory the model needs. Then ask what that card costs right now.

A 24 GB consumer card such as an RTX 4090 is a sound first machine for ComfyUI and for proving a LoRA run. A 32 GB RTX 5090 leaves more room for image and video work without jumping straight to a datacenter part. A 70B-class chat model, or vLLM with a long context, usually wants the 80 GB on an H100. If the context or the batch no longer fits in 80 GB, look at the 141 GB H200.

A cheaper card does not fix a memory miss. The process runs out of VRAM while loading weights or stretching context. Move up a memory class instead of retrying the same card. The GPU list (https://novapod.io/gpus) shows which models are offered and what they ask. A model’s price page says what that memory is for. The offer on the marketplace (https://novapod.io/marketplace) is the machine you can actually launch this time.

The starting ask on a price page comes from the catalog and is there for comparison. Before you rent, use the offer you can still click on the marketplace. When the two numbers differ, use the one that can boot.

## Asks, medians, and the per-second bill

The hourly price is how the quote is written. Once the machine is running, the balance is charged per second. Stopping the machine stops that GPU charge. Leaving it idle does not.

A low price only helps if the machine stays up. An ask far below the median is a reasonable smoke test: the image boots, the port opens, and one request returns. It is not automatically a machine to leave on production traffic all day. A higher ask with a shorter queue can cost less for an online service, because users wait on latency, not on the hourly figure printed on a card.

Before a long job, write down three lines: the GPU name, the ask you accepted, and the template. The next boot uses those lines, not an old screenshot.

## Deposits: set the USDT value, then convert the coin

Add credits is the deposit screen. The minimum transfer is $100. Below that, Continue stays disabled and the API does not issue a deposit address. That floor is per transfer. It is not a rule that a smaller payment sits aside until later transfers add up.

You choose a dollar amount. Packages start at $150. A custom amount is fine at $100 or more. After the amount, you choose the network. One hundred and fifty dollars is a USDT-denominated credit. It does not mean “send 150 coins on every chain.”

USDT and USDC quantities match the dollar amount. One stablecoin unit is one dollar of credit. For SOL, ETH, or BNB, the backend converts that dollar amount with the current USDT price of the coin. The large figure on the page is that quantity, for example a SOL amount, with the line that says what one coin is worth in USDT. The QR code carries the same quantity. Switching among SOL, ETH, and BNB recalculates it.

Prices refresh about every 20 seconds. If the feed is down, the page should not tell you to send “$150 of SOL” without a quantity. Without a quantity, do not send the native coin. A wallet or an exchange cannot match an unspecified amount.

Keep the chain and the token together. USDT on TRON is a different payment from USDT on Ethereum. SOL and USDC on Solana use the Solana address. ETH, BNB, and EVM stablecoins use the 0x address. Send only the token and chain printed next to the address. A mismatch is not credited automatically, and support cannot recover it by asking for a private key. Do not send a seed phrase or a private key to anyone, including support.

Credit follows what arrives, not the package button you clicked. Bonuses apply to each incoming transfer: 3% from $200, 5% from $500, 7% from $1,000, 10% from $1,500, and 15% from $2,000. A $150 transfer has no bonus. The balance pays for GPU time under the site’s credit rules.

Wait for the network confirmation before you decide the deposit failed. If it still does not show, check the token, the chain, that the amount is at least $100, and that the destination is the address on the page. Then email the transaction hash, chain name, amount, deposit address, and account email to support@novapod.io.

## From an account to the first machine

Registration creates the account only after the email code is verified. The password needs at least 12 characters and both letters and numbers. A symbol is optional, so a password suggested by the browser can be used. Sign-in asks for the email first, then the password. An account with a passkey can use that instead. Google and GitHub are on the sign-in page.

RENT NOW on the marketplace sends a signed-out visitor to the sign-in page and, after login, back to that rental page. A rental without a session is not accepted.

Boot the first machine from a template instead of installing CUDA on an empty disk. The template list (https://novapod.io/templates) includes images such as vLLM, ComfyUI, and PyTorch. The workload notes are:

- vLLM: https://novapod.io/workloads/vllm
- LoRA: https://novapod.io/workloads/lora
- ComfyUI: https://novapod.io/workloads/comfyui

A practical order is: read the GPU list, open the price page for memory and fit, accept one live offer, deposit at least $100, start from a template, run one low-concurrency or short training check, and only then add traffic or time.

## How to start the three common jobs

For an open model behind an API, follow the vLLM notes. Confirm the weights and context fit the card, boot the template, and send one short completion. Check the JSON shape and the timeout. Raise concurrency from 1. If memory runs out, shorten the context or move up a VRAM class. Do not keep a 70B model on a 24 GB card. Point a production name at the pod only after that single request is stable. Shut the machine off when requests stop.

For LoRA, prove a short step on one GPU: the data, the tokenizer, whether loss falls, and whether a checkpoint is written. An RTX 4090 is a reasonable place for that step. Consider an H100 after it works. A training image and a serving image are different boots. After the adapter is exported, stop the training machine if you are done with it.

For images or video, use ComfyUI. Load one known workflow and confirm model paths and samplers. Change resolution or batch size one setting at a time. An RTX 4090 or RTX 5090 is enough to debug the graph. Move to a larger card when the graph is right and you need throughput. Stop the pod after you export the outputs. An open ComfyUI window with no jobs still burns seconds.

All three jobs need the same note: GPU name, ask, and template. Those three lines are what you use when something fails. “The machine is broken” is not.

## MCP for an agent

When the caller is Cursor or Claude instead of a person in the browser, use MCP. The page is https://novapod.io/mcp and the endpoint is https://novapod.io/api/mcp.

Listing GPUs and live asks, reading one GPU, and listing templates do not need a key. Balance, active rentals, creating a rental, and the deposit address need an API key from the console. The key starts with `prlc_` and goes in `Authorization: Bearer`.

A rental defaults to one GPU and spends crypto credit. Region and image fall back to the first configured option. The deposit-address tool returns an address and never a private key. The agent should not be asked to store a seed phrase.

The agent’s order matches a person’s: call list_gpus and pick a slug by VRAM, call list_templates, read the balance, and if it is short, fetch the deposit address and send at least $100 of value. Then call create_rental. Asks from MCP are the same asks as the marketplace.

## When this market is the wrong tool

NovaPod fits spot use of one GPU or a small count: one serving run, one fine-tune, one image batch. It is not a three-year quote for thousands of cards. Asks move, and a very cheap machine can still be a poor place to leave a job overnight.

A transfer on the wrong chain is not treated as the deposit you intended. Handing a private key to a script or to support does not speed up credit. An hourly figure in an article, a comparison page, or an old screenshot does not replace the number on the marketplace at the moment you click.

The site already has comparison notes for Vast.ai, RunPod, and Lambda. Those pages describe deposits, templates, and per-second billing. The price you will pay is still on the H100 SXM and RTX 4090 price pages.

## The price table and the marketplace are different lists

The price table (https://novapod.io/pricing) lines up VRAM, compute, and a starting hourly figure so you can compare an H200, an H100, an A100, and a 4090 against the model you want to run. The marketplace lists machines you can rent now. The same model name in both places does not mean the two figures must match. The table narrows the choice. The marketplace sets what this rental costs.

Per-second billing covers time the GPU is running. After the export or the download, stop the machine from the rentals list. Leaving a training pod up as an inference server usually means paying for the wrong image. For serving, boot a vLLM template on a card that fits.

## Who can place an order

A new account is created only after the email code is verified. The password is at least 12 characters and includes letters and numbers. A symbol is not required, so a browser-suggested password can pass. Sign-in collects the email first, then the password. An account that already has a passkey can use it.

RENT NOW while signed out opens the sign-in page and returns to the rental page after login. Balance, current machines, and the deposit address belong to that account. Browsing the GPU list and the templates does not require a deposit first.

## What to keep out of the agent setup

MCP is for letting Cursor or Claude read prices and place a rental from the chat. It is a poor place to keep a wallet. Put the key only in the local MCP config, as `Authorization: Bearer`, using a `prlc_` key from the console. Do not paste that key into the chat transcript.

Public calls can list cards, prices, and templates. Calls that move money need the key. Creating a rental defaults to one GPU and spends crypto credit through the same order path as the site. If you do not name a region or image, the service uses a configured default. The deposit address can be read. A private key is not in the response.

If the balance is short, have the agent read the address, send at least $100 of value yourself from a wallet or an exchange, wait until it is credited, and only then create the rental. Do not let the model invent a destination address.

After the job, stop the machine. The balance falls per second. Stopping on time saves more than hunting for a lower hourly ask after the fact.

## Where to start

This order is enough:

1. Models and asks: https://novapod.io/gpus
2. What one card is for, for example https://novapod.io/pricing/h100-sxm or https://novapod.io/pricing/rtx-4090
3. Rent on the marketplace: https://novapod.io/marketplace
4. Deposit: after sign-in, open Add credits, use at least $100, and send the coin and quantity the page shows
5. Templates: https://novapod.io/templates
6. Agent access, when you need it: https://novapod.io/mcp
