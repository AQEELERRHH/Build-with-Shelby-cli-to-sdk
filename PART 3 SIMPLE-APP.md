# Part 3: Building a Simple App with Shelby (Node.js)

This is Part 3 of the beginner-friendly Shelby learning series.

- Part 1: Using the Shelby CLI
- Part 2: Using the Shelby SDK with Node.js
- Part 3 (this guide): Using Shelby inside a simple app

In this part, we’ll build a very small app that lets a user:

- Upload files
- View uploaded files
- Download files later

No frontend frameworks.
No complex setup.
Just a clean, simple example to show how Shelby fits into real apps.

##  Goal of This Part

By the end of this guide, you will:

- Understand what a “Shelby-powered app” looks like
- Use the Shelby SDK inside an app flow
- Build a simple file upload & retrieval app
- See how this can later grow into games, dashboards, or dApps

##  What Kind of App Are We Building?

We are building a command-based app that behaves like this:

1. User chooses an action:
   - Upload a file
   - List files
   - Download a file
2. The app performs the action using Shelby
3. The app shows the result

This is intentionally simple the focus is Shelby integration, not UI design.

##  Prerequisites

Before starting, make sure you have:

- Completed Part 2 (SDK Basics)
- Node.js installed
- A funded Shelby account
- Basic terminal usage

You do not need React, Next.js, or blockchain knowledge.

##  Step 1: Project Setup

Create a new folder:

```bash
mkdir shelby-simple-app
cd shelby-simple-app
```

Initialize Node.js:

```bash
npm init -y
```

Install dependencies:

```bash
npm install @shelbyxyz/sdk dotenv readline-sync
```

What these do:

- `@shelbyxyz/sdk` → Shelby integration
- `dotenv` → environment variables
- `readline-sync` → simple user input

##  Step 2: Environment Variables

Create a `.env` file:

```bash
touch .env
```

Add:

```env
SHELBY_PRIVATE_KEY=your_private_key_here
SHELBY_NETWORK=testnet
```

Never commit this file to GitHub.

##  Step 3: App Structure

Create a file:

```bash
touch app.js
```

Your project should now look like this:

```text
shelby-simple-app/
├─ app.js
├─ package.json
├─ .env
└─ node_modules/
```

## Step 4: Connecting to Shelby

Open `app.js` and add:

```js
import { ShelbyClient } from "@shelbyxyz/sdk";
import "dotenv/config";
import readline from "readline-sync";

const client = new ShelbyClient({
  privateKey: process.env.SHELBY_PRIVATE_KEY,
  network: process.env.SHELBY_NETWORK,
});
```

This sets up the Shelby client for the app.

##  Step 5: App Menu

Add this below the client:

```js
function showMenu() {
  console.log("\n=== Shelby Simple App ===");
  console.log("1. Upload a file");
  console.log("2. List files");
  console.log("3. Download a file");
  console.log("4. Exit");
}
```

This is how users interact with the app.

##  Step 6: Upload Function

Add:

```js
async function uploadFile() {
  const path = readline.question("Enter file path: ");
  const result = await client.files.upload({ path });
  console.log("Uploaded:", result);
}
```

##  Step 7: List Files Function

Add:

```js
async function listFiles() {
  const files = await client.files.list();
  console.log("\nYour files:");
  files.forEach((file, index) => {
    console.log(`${index + 1}. ${file.id}`);
  });
  return files;
}
```

##  Step 8: Download Function

Add:

```js
async function downloadFile() {
  const files = await listFiles();
  if (files.length === 0) return;

  const choice = readline.questionInt("Choose file number: ");
  const selected = files[choice - 1];

  await client.files.download({
    fileId: selected.id,
    outputPath: `./downloaded-${choice}.txt`,
  });

  console.log("Download complete");
}
```

##  Step 9: App Loop

Add at the bottom of `app.js`:

```js
async function main() {
  while (true) {
    showMenu();
    const choice = readline.questionInt("Select an option: ");

    if (choice === 1) await uploadFile();
    else if (choice === 2) await listFiles();
    else if (choice === 3) await downloadFile();
    else if (choice === 4) break;
    else console.log("Invalid option");
  }
}

main().catch(console.error);
```

##  Step 10: Run the App

```bash
node app.js
```

You now have a working Shelby-powered app 🎉

##  Why This Matters

This app proves that:

- Shelby is not “just file uploads”
- It can power apps, games, dashboards, and workflows
- The same logic can later be used in:
  - Web apps
  - dApps
  - Games with progression
  - Data storage platforms
