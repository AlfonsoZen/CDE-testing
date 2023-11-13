# Introduction 
Automated testing is considered an essential part of any serious software development effort. Automation makes it easy to repeat individual tests or test suites quickly and easily during development. __This helps ensure that releases meet quality and performance goals.__

# Jest
[Jest](https://jestjs.io/) is a delightful JavaScript Testing Framework with a focus on simplicity.

It works with projects using several Frameworks, for purposes of this project, we'll review the implementation in the followings Frameworks:
- [Next.js](https://nextjs.org/)
- [Nest.js](https://nestjs.com/) 
- [Remix](https://remix.run/)

> **Disclaimer:** Make sure you are using the same versions as this tutorial:
> -  Node: 20.8
> - Nest CLI: 10.2.1
> - Latest Jest: 29.1.0
> - TypeScript: 5.1.3

---
# Nest.js 
Nest ([Nest.js](https://nestjs.com/)) is a framework for building efficient, scalable [Node.js](https://nodejs.org/) server-side applications. It uses progressive JavaScript, is built with and fully supports [TypeScript](http://www.typescriptlang.org/)
### Prerequisites
- Latest Nest version: `"@nestjs/common": "^10.0.0",`
- Please make sure that [Node.js](https://nodejs.org/) (version >= 16) is installed on your operating system.

#### Installation
To scaffold the project with the Nest CLI, run the following commands.
```sh
$ npm i -g @nestjs/cli
$ nest new project-name
```

> **HINT:** To create a new TypeScript project with stricter feature set, pass the `--strict` flag to the `nest new` command.

#### Running the application
Once the installation process is complete, you can run the following command at your OS command prompt to start the application listening for inbound HTTP requests:
```sh
$ npm run start
```

Once the application is running, open your browser and navigate to `http://localhost:3000/`. You should see the `Hello World!` message.

To watch for changes in your files, you can run the following command to start the application:
```bash
$ npm run start:dev
```

This command will watch your files, automatically recompiling and reloading the server.

## Testing: Implementing Jest
[Jest](https://github.com/facebook/jest) is provided as the default testing framework by Nest. It serves as a test-runner and also provides assert functions and test-double utilities that help with mocking, spying, etc.
#### Installation
To get started, first install the required package:
```bash
$ npm i --save-dev @nestjs/testing
```

### Default Unit Test:
The boilerplate created by the Nest CLI already implements a unit test for our "Hello World!" which should look like this:
```tsx
import { Test, TestingModule } from '@nestjs/testing';
import { AppController } from './app.controller';
import { AppService } from './app.service';

describe('AppController', () => {
	let appController: AppController;

	beforeEach(async () => {
		const app: TestingModule = await Test.createTestingModule({
			controllers: [AppController],
			providers: [AppService],
		}).compile();

		appController = app.get<AppController>(AppController);
	});

	describe('root', () => {
		it('should return "Hello World!"', () => {
			expect(appController.getHello()).toBe('Hello World!');
		});
	});
});
```

Such test can be tested by running: 
```sh
npm run test
```

Which should print something as follows: 
![[Pasted image 20231110124126.png]]

### HTTP Verb Test: 
Based on the structure of the default unit test, let's provide examples for testing different HTTP verbs.

> __Disclaimer__:  The following examples are based on my research. I have not yet implemented them in a real-world application.
#### DELETE Example:
Assuming you have a controller with a delete endpoint (e.g., `deleteItem` in `ItemController`):
```tsx
describe('ItemController', () => {
  // ... (similar setup)

  describe('deleteItem', () => {
    it('should delete an item by ID', async () => {
      const itemId = 'someItemId';

      // Assuming you have a method in your service to delete an item
      const deletedItem = await itemController.deleteItem(itemId);

      // Assert the result
      expect(deletedItem).toBeDefined();
      // Add more specific assertions based on your item structure or the expected result of deletion
    });
  });
});
```
**Description:** This example tests the `deleteItem` endpoint of the `ItemController` to ensure that it successfully deletes an item identified by its ID. It checks if the method in the service responsible for item deletion is functioning correctly.

#### GET Example:
Assuming you have a controller with a get endpoint (e.g., `getItem` in `ItemController`):
```tsx
describe('ItemController', () => {
  // ... (similar setup)

  describe('getItem', () => {
    it('should get an item by ID', async () => {
      const itemId = 'someItemId';

      // Assuming you have a method in your service to get an item
      const foundItem = await itemController.getItem(itemId);

      // Assert the result
      expect(foundItem).toBeDefined();
      expect(foundItem.id).toBe(itemId);
      expect(foundItem.name).toBe('Expected Item Name');
      // Add more specific assertions based on your item structure
    });
  });
});
```
**Description:** This example tests the `getItem` endpoint of the `ItemController` to ensure that it successfully retrieves an item by its ID. It checks if the method in the service responsible for item retrieval is functioning correctly.

#### PATCH Example:
Assuming you have a controller with a patch endpoint (e.g., `updateItem` in `ItemController`):
```tsx
describe('ItemController', () => {
  // ... (similar setup)

  describe('updateItem', () => {
    it('should update an item', async () => {
      const itemId = 'someItemId';
      const updatedData = {
        name: 'Updated Item Name',
        // Add other properties as needed
      };

      // Assuming you have a method in your service to update an item
      const updatedItem = await itemController.updateItem(itemId, updatedData);

      // Assert the result
      expect(updatedItem).toBeDefined();
      expect(updatedItem.name).toBe('Updated Item Name');
      // Add more specific assertions based on your item structure
    });
  });
});
```
**Description:** This example tests the `updateItem` endpoint of the `ItemController` to ensure that it successfully updates an item identified by its ID with the provided data. It checks if the method in the service responsible for item updating is functioning correctly.

#### POST Example:
Assuming you have a controller with a post endpoint (e.g., `createItem` in `ItemController`):
```tsx
describe('ItemController', () => {
  // ... (similar setup)

  describe('createItem', () => {
    it('should create a new item', async () => {
      const newItemData = { /* your new item data */ };

      // Assuming you have a method in your service to create an item
      const createdItem = await itemController.createItem(newItemData);

      // Assert the result or check the side effects
      expect(createdItem).toBeDefined();
      // Add more assertions as needed
    });
  });
});
```
**Description:** This example tests the `createItem` endpoint of the `ItemController` to ensure that it successfully creates a new item with the provided data. It checks if the method in the service responsible for item creation is functioning correctly.

---
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
