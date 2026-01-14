## Guide to Clone the Project

```bash
git clone https://github.com/farrasnazhif/express-setup.git
```

Install dependencies.

```bash
npm install
```

Start the server.

```bash
npm run server
```

## Guide to Setting Up a Basic Express Server with TypeScript

This guide will help you create a simple Express.js server using TypeScript, starting from project setup all the way to running it in your browser.

## Prerequisites

Before you begin, make sure you already have these installed on your machine:

Node.js (Latest LTS recommended)  
npm (or yarn / pnpm)

### 1. Project Initialization

Initialize the project so Node.js can manage your dependencies.

This will create a `package.json` file that stores your project info, scripts, and dependencies.

```bash
npm init -y
```

### 2. Install Dependencies

install Express and the tools needed to work with TypeScript.

Install Express (the main framework for your server).

```bash
npm install express
```

Install TypeScript, the necessary type definitions, and helper tools to run TypeScript directly without compiling manually.

```bash
npm install -D typescript tsx @types/node ts-node @types/express nodemon
```

### 3. Configure TypeScript

Create a `tsconfig.json` file in your project root to configure the TypeScript compiler. You can generate a default file using the following command.

```bash
npx tsc --init
```

For a basic setup, make sure your `tsconfig.json` includes at least these settings:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "nodenext",
    "moduleResolution": "nodenext",
    "outDir": "./dist",
    "rootDir": "./",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["./**/*.ts"],
  "exclude": ["node_modules"]
}
```

### 4. Create the Server File

Create your main server file, for example `server.ts`.

Add a basic route so you can test if the server is working with this following code:

```typescript
import express, { Request, Response } from "express";

const app = express();

const port = 3000;

app.get("/", (req: Request, res: Response) => {
  res.send("Server is Live!");
});

app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});
```

### 5. Update package.json Scripts

Modify your `package.json` file to add scripts for starting the server using `tsx`.

This will also ensure whenever we have changes, the server automatically follow the updates.

```json
"scripts": {
    "start": "tsx server.ts",
    "server": "nodemon --exec tsx server.ts",
    "build": "tsc"
}
```

```json
"type": "module"
```

### 6. CORS Setup

When your frontend (React/Vue) and backend (Express) talk to each other, they’re often running on different origins during development, for allowing requests by default, that's where CORS comes in.

Update the `server.ts` with this following code:

```typescript
import express, { Request, Response } from "express";
import cors from "cors";

const port = process.env.PORT || 5173;

const app = express();

app.use(cors());
app.use(express.json());

app.get("/", (req: Request, res: Response) => {
  res.send("Server is Live!");
});

app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});
```

Install CORS:

```bash
npm install cors dotenv
```

```bash
npm install -D @types/cors
```

### 7. Run the Server

Start your server using the new script:

```bash
npm run server
```

You should see the message: Server is running at http://localhost:3000

Open your web browser and navigate to http://localhost:3000 to see the

"Server is Live!" message.
