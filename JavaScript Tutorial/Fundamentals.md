# Makefile for JavaScript Tutorial Project

# Variables
NODE_MODULES = node_modules
SRC_DIR = src
DIST_DIR = dist
TESTS_DIR = tests
DOCS_DIR = docs
PORT = 3000

# Phony targets
.PHONY: install clean lint test build serve watch docs format help

# Default target
help:
	@echo "JavaScript Tutorial Project Makefile"
	@echo "Available commands:"
	@echo "  make install    - Install dependencies"
	@echo "  make clean      - Remove build artifacts"
	@echo "  make lint       - Run linter"
	@echo "  make test       - Run tests"
	@echo "  make build      - Build project (lint+test+build)"
	@echo "  make serve      - Start dev server on port 3000"
	@echo "  make watch      - Watch for changes"
	@echo "  make docs       - Generate documentation"
	@echo "  make format     - Format code"
	@echo "  make help       - Show this help"

install:
	@echo "Installing dependencies..."
	npm install
	@echo "Done."

clean:
	@echo "Cleaning..."
	rm -rf $(DIST_DIR) $(NODE_MODULES)
	@echo "Done."

lint:
	npx eslint $(SRC_DIR) $(TESTS_DIR)

test:
	npx jest --coverage

build: lint test
	npx webpack --mode production

serve:
	npx webpack serve --port $(PORT) --open

watch:
	npx webpack --watch

docs:
	npx jsdoc $(SRC_DIR) -d $(DOCS_DIR)

format:
	npx prettier --write "**/*.{js,json,md}"