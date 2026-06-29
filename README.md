# Ignot-bank-statement-
name: Generate INGOT statement PDF

on:
  push:
    branches:
      - 'add/ingot-statement-pdf-workflow'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
      - name: Install dependencies
        working-directory: docs
        run: npm ci
      - name: Generate PDF
        working-directory: docs
        run: npm run generate
      - name: Upload PDF artifact
        uses: actions/upload-artifact@v4
        with:
          name: ingot-statement-pdf
          path: docs/ingot-statement.pdf
