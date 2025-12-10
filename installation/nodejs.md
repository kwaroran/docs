# Node.js

!!! Note
These steps assume that you have already installed Node.js and Git on your system.
!!!

Run RisuAI locally using Node.js for development or self-hosting purposes.

## Prerequisites

- [Node.js](https://nodejs.org/) (v20 or higher recommended)
- [Git](https://git-scm.com/)

## Installation

1. Clone the repository
   ```bash
   git clone https://github.com/kwaroran/RisuAI.git
   cd RisuAI
   ```

2. Install dependencies
   ```bash
   npm install
   ```

3. Start the development server
   ```bash
   npm run dev
   ```

4. Open your browser and navigate to `http://localhost:5173`

## Building for Production

To build RisuAI for production:

```bash
npm run build
```

The built files will be in the `dist` directory.

## Updating

To update to the latest version:

```bash
git pull
npm install
```
