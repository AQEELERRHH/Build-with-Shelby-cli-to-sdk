# Part 2: Shelby SDK Basics (Node.js)

This guide is Part 2 of the beginner friendly Shelby learning series.

In Part 1, we learned how to interact with Shelby using the CLI by running commands in the terminal.
In this part, we will learn how to do similar things using the Shelby SDK with Node.js.

Don’t worry if you are not a developer we will move slowly and explain each step clearly.

##  What You’ll Learn in This Part

By the end of this guide, you will understand:

- What the Shelby SDK is
- When to use the SDK instead of the CLI
- How to set up a simple Node.js project
- How to connect to Shelby using the SDK
- How to perform basic file operations using code

##  What Is the Shelby SDK?

The Shelby SDK is a set of tools that allows you to interact with Shelby using code instead of terminal commands.

Think of it like this:

- CLI → You type commands manually
- SDK → You write small scripts that do the work for you

### When should you use the SDK?

- When building an app
- When automating tasks
- When you want Shelby actions to run inside a program

The CLI is great for learning.
The SDK is better for building things.

##  Prerequisites

Before starting, make sure you have:

- Node.js installed (version 18 or higher recommended)
- Basic knowledge of using the terminal
- Completed Part 1 (CLI Basics) or understand how accounts and funding work

You do not need advanced JavaScript knowledge.

##  Step 1: Create a New Project Folder

First, create a new folder for this project.

```bash
mkdir part2-sdk-basics
cd part2-sdk-basics
```

This folder will hold all our files.

##  Part 2 Folder Structure

Use this folder layout for Part 2:

```text
part2-sdk-basics/
├── README.md
├── package.json
├── index.js
└── files/
    └── hello.txt
```

##  Step 2: Initialize a Node.js Project

Run the following command:

```bash
npm init -y
```

This creates a `package.json` file, which helps Node.js manage dependencies.

You don’t need to edit this file manually for now.

##  Step 3: Install the Shelby SDK

Now install the Shelby SDK:

```bash
npm install @shelbyxyz/sdk
```

This downloads the SDK and makes it available in your project.

##  Step 4: Environment Setup

Just like in Part 1, the SDK needs access to your account credentials.

Create a `.env` file in your project root:

```bash
touch .env
```

Inside the file, add your credentials (example):

```env
SHELBY_PRIVATE_KEY=your_private_key_here
SHELBY_NETWORK=testnet
```

⚠️ Important:
Never commit your private key to GitHub.

##  Understanding the SDK Client

The SDK works by creating a client.

The client:

- Authenticates your account
- Connects to the Shelby network
- Allows you to perform actions like uploads and downloads

You will usually create one client and reuse it.

## 👋 Step 5: Your First Shelby SDK Script

Create a new file:

```bash
touch index.js
```

Inside `index.js`, add:

```js
import { ShelbyClient } from "@shelbyxyz/sdk";
import "dotenv/config";

async function main() {
  const client = new ShelbyClient({
    privateKey: process.env.SHELBY_PRIVATE_KEY,
    network: process.env.SHELBY_NETWORK,
  });

  const account = await client.account.getInfo();
  console.log("Connected account:", account);
}

main().catch(console.error);
```

Run the script:

```bash
node index.js
```

If everything is set up correctly, you should see your account information printed.

This confirms:

- The SDK is installed
- Your credentials work
- You are connected to Shelby

## Step 6: Uploading a File Using the SDK

Create a small test file:

```bash
mkdir -p files
echo "Hello Shelby SDK" > files/hello.txt
```

Update `index.js`:

```js
const upload = await client.files.upload({
  path: "./files/hello.txt",
});

console.log("File uploaded:", upload);
```

Run again:

```bash
node index.js
```

You have now uploaded a file using code instead of the CLI.

## Step 7: Listing Files

To list your uploaded files:

```js
const files = await client.files.list();
console.log("Your files:", files);
```

This is the SDK equivalent of listing files from the CLI.

##  Step 8: Downloading a File

To download a file:

```js
await client.files.download({
  fileId: files[0].id,
  outputPath: "./downloaded.txt",
});

console.log("File downloaded");
```

This saves the file locally.

##  Common Beginner Issues

- Node version too old → Upgrade Node.js
- Missing `.env` variables → Check spelling
- Permission errors → Ensure account is funded
- Import errors → Confirm SDK is installed correctly

If something breaks, re-check each step calmly.

##  CLI vs SDK (Quick Comparison)

| Task | CLI | SDK |
|---|---|---|
| Learning basics | ✅ | ⚠️ |
| Automation | ❌ | ✅ |
| App integration | ❌ | ✅ |
| One-off commands | ✅ | ❌ |

##  What’s Next?

In Part 3, we will:

- Build a small real-world script
- Automate uploads
- Explore how this can fit into a simple app

You don’t need to rush, understanding the basics is more important than speed.

## NOTE: Getting an API Key (from part1, incase you dont know how to)
Go to https://geomi.dev/

Create an account

Go to Overview

Click Create API Keys

Fill in the form:

Network: Select Shelbynet
Resource Name: Any descriptive name
Usage Description: Short explanation of how you’ll use Shelby
Create the API key

Copy the API key and paste it into your terminal when prompted. 

https://x.com/aqeelerh  LEAVE A REVIEW
