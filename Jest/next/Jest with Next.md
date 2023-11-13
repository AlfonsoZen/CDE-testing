
# Next.js 
[Nest.js](https://nextjs.org/) is a React framework for building full-stack web applications. You use React Components to build user interfaces, and Next.js for additional features and optimizations.

### Prerequisites
- Node.js 18.17 or later.
- macOS, Windows (including WSL), and Linux are supported.

#### Automatic Installation
To create a project, run:
```sh
npx create-next-app@latest
```

On installation, you'll see the following prompts:
```sh
What is your project named? my-app
Would you like to use TypeScript? No / Yes
Would you like to use ESLint? No / Yes
Would you like to use Tailwind CSS? No / Yes
Would you like to use `src/` directory? No / Yes
Would you like to use App Router? (recommended) No / Yes
Would you like to customize the default import alias (@/*)? No / Yes
What import alias would you like configured? @/*
```

After the prompts, `create-next-app` will create a folder with your project name and install the required dependencies.

#### Running the application
1. Run `npm run dev` to start the development server.
2. Visit `http://localhost:3000` to view your application.
3. Edit `app/layout.tsx` (or `pages/index.tsx`) file and save it to see the updated result in your browser.
## Testing: Implementing Jest
[Jest](https://github.com/facebook/jest) and React Testing Library are frequently used together for **Unit Testing**.
#### Installation
You can use `create-next-app` with the [with-jest](https://github.com/vercel/next.js/tree/canary/examples/with-jest) example to quickly get started with Jest and React Testing Library:
```bash
npx create-next-app@latest --example with-jest with-jest-app
```

#### Setting up Jest (with the Rust Compiler)
Since the release of [Next.js 12](https://nextjs.org/blog/next-12), Next.js now has built-in configuration for Jest.

To set up Jest, install `jest`, `jest-environment-jsdom`, `@testing-library/react`, `@testing-library/jest-dom`:
```sh
npm install --save-dev jest jest-environment-jsdom @testing-library/react @testing-library/jest-dom
```

Create a `jest.config.mjs` file in your project's root directory and add the following:
```jsx
import nextJest from 'next/jest.js'
 
const createJestConfig = nextJest({
  // Provide the path to your Next.js app to load next.config.js and .env files in your test environment
  dir: './',
})
 
// Add any custom config to be passed to Jest
/** @type {import('jest').Config} */
const config = {
  // Add more setup options before each test is run
  // setupFilesAfterEnv: ['<rootDir>/jest.setup.js'],
 
  testEnvironment: 'jest-environment-jsdom',
}
 
// createJestConfig is exported this way to ensure that next/jest can load the Next.js config which is async
export default createJestConfig(config)
```
