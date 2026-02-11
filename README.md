# Build with Shelby

A beginner-friendly tutorial series for learning Shelby step by step.

## Repository structure

```text
build-with-shelby/
├── README.md
├── part1-cli-basics/
│   └── README.md
└── part2-sdk-basics/
    └── README.md
```
# Part 1: Shelby CLI Basics

This guide is for complete beginners.

You do not need blockchain experience. If you can open a terminal and copy commands, you can follow along.

## What is the Shelby CLI?

The Shelby CLI is a command-line tool that lets you upload, store, and download files using the Shelby decentralized storage network.

In simple terms:

- You type commands in your terminal
- The Shelby CLI runs those commands
- Shelby handles file storage and retrieval behind the scenes

## Mental model: how Shelby handles your files

Think of Shelby as a file shipping service:

- Your computer → sender
- Shelby network → shipping company
- Storage nodes → warehouses
- Blob name → package label

### The basic flow

Local file → Shelby network → Storage nodes → Blob name → Download

You upload a file from your machine, Shelby stores it across the network, and you later retrieve it using the same account.

The CLI is simply your control panel for this process.

## When should I use the CLI?

Use the Shelby CLI when you want to:

- Upload files from your laptop or server
- Script or automate storage workflows
- Learn how Shelby works without a UI
- Test uploads before building an app

Why beginners like it:

- Commands are copy-paste friendly
- Fast feedback
- Clear mental model of storage actions

## Prerequisites

Before starting, make sure you have:

- Node.js (v18+ recommended)
- Internet access
- A terminal (Linux, macOS, or WSL)

## Install the Shelby CLI

Shelby CLI is installed using a Node.js package manager.

### Install with npm (recommended)

```bash
npm install -g @shelby-protocol/cli
```

Alternative options:

```bash
pnpm add -g @shelby-protocol/cli
yarn add -g @shelby-protocol/cli
bun add -g @shelby-protocol/cli
```

### Verify installation

```bash
shelby --version
```

If a version number prints, installation was successful.

## Initialize Shelby

Before using the CLI, you must initialize it.

```bash
shelby init
```

This step:

- Creates a config file at `~/.shelby/config.yaml`
- Sets up your Shelby account
- May prompt you for an API key or environment setup

Follow the prompts shown in your terminal.

## Fund your account (important)

Shelby operations require tokens:

- Aptos tokens → network gas
- ShelbyUSD tokens → storage payments

The official docs provide faucet commands to get test tokens.

👉 Follow the funding steps here:
https://docs.shelby.xyz/tools/cli

⚠️ Uploads will fail if your account is not funded.

## Upload your first file

### Create a test file

```bash
echo "Hello from Shelby CLI" > hello.txt
```

### Upload the file

Shelby uploads require:

- A source file
- A destination blob name
- An expiration time

Example:

```bash
shelby upload hello.txt hello.txt -e "tomorrow"
```

What this does:

- Uploads `hello.txt`
- Stores it under the name `hello.txt`
- Sets an expiration time for the file

After a successful upload, Shelby confirms the operation in the terminal.

## List your uploaded files

To see files uploaded by your account:

```bash
shelby account blobs
```

This lists:

- Blob names
- Sizes
- Expiration times

This is the main way to verify uploads using the CLI.

## Download a file

You can download files that were uploaded by your active account.

```bash
shelby download hello.txt downloaded-hello.txt
```

Check the contents:

```bash
cat downloaded-hello.txt
```

Expected output:

```text
Hello from Shelby CLI
```

## Important limitations (CLI)

- The CLI currently allows downloading only files uploaded by your account
- Expired files cannot be downloaded
- Blob names must match exactly

## What happens behind the scenes?

When you run an upload command, the CLI:

1. Reads the local file
2. Packages file data and metadata
3. Sends it to Shelby services
4. Pays required storage fees
5. Registers the blob on the network

You don’t manage storage nodes directly — Shelby handles that.

## Common beginner issues

### `shelby: command not found`

- CLI not installed correctly
- Restart your terminal
- Re-run install command

### Upload fails with payment error

- Account not funded
- Get Aptos + ShelbyUSD tokens from the faucet

### File not found

- Wrong directory
- Confirm file exists:

```bash
ls
```

### Blob not listed

- Upload failed
- Blob expired
- Different active account

## Accuracy note

Shelby CLI commands and flags may evolve.

Always confirm details with:

- `shelby --help`
- Official docs: https://docs.shelby.xyz

## Quick recap

You learned how to:

- Install the Shelby CLI
- Initialize an account
- Fund your account
- Upload a file
- List stored blobs
- Download a file

➡️ In Part 2, we’ll do the same workflow using a Shelby SDK inside application code.
