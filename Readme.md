# nr

Managing projects with multiple package managers can be a pain. `nr` is a simple shell function that helps you run npm, pnpm, bun, or yarn scripts without having to remember which package manager to use.

## Installation

Add the following to your `.zshrc` or `.bashrc` file:

```zsh
# Function to run npm, pnpm, bun, or yarn scripts
function nr() {
  if [[ -f "pnpm-lock.yaml" ]]; then
    echo ">> pnpm run $@"
    pnpm run "$@"
  elif [[ -f "bun.lockb" ]]; then
    echo ">> bun run $@"
    bun run "$@"
  elif [[ -f "yarn.lock" ]]; then
    echo ">> yarn run $@"
    yarn run "$@"
  elif [[ -f "package-lock.json" ]]; then
    echo ">> npm run $@"
    npm run "$@"
  else
    echo "❌ Not a valid project directory"
  fi
}

# Function to alias npx, pnpx, bunx, or yarn
function nx() {
  if [[ -f "pnpm-lock.yaml" ]]; then
    echo ">> pnpx $@"
    pnpx "$@"
  elif [[ -f "bun.lockb" ]]; then
    echo ">> bunx $@"
    bunx "$@"
  elif [[ -f "yarn.lock" ]]; then
    echo ">> yarn $@"
    yarn "$@"
  elif [[ -f "package-lock.json" ]]; then
    echo ">> npx $@"
    npx "$@"
  else
    echo "❌ Not a valid project directory"
  fi
}

# Function to install packages using npm, pnpm, bun, or yarn
function ni() {
  if [[ -f "pnpm-lock.yaml" ]]; then
    echo ">> pnpm install $@"
    pnpm install "$@"
  elif [[ -f "bun.lockb" ]]; then
    echo ">> bun install $@"
    bun install "$@"
  elif [[ -f "yarn.lock" ]]; then
    echo ">> yarn install $@"
    yarn install "$@"
  elif [[ -f "package-lock.json" ]]; then
    echo ">> npm install $@"
    npm install "$@"
  else
    echo "❌ Not a valid project directory"
  fi
}
```

Now you can run `nr`, `nx`, and `ni` in your project directory.

# Usage

- `nr <script>` - Run a script using the appropriate runtime.

  - Running `nr start` will run `npm run start` or `pnpm run start` or `bun run start` or `yarn run start` depending on the runtime of your project.

- `nx <command>` - Run a command using the appropriate runtime.

  - Running `nx create-react-app my-app` will run `npx create-react-app my-app` or `pnpx create-react-app my-app` or `bunx create-react-app my-app` or `yarn create-react-app my-app` depending on the runtime of your project.

- `ni <package>` - Install a package using the appropriate runtime.
  - Running `ni react` will run `npm install react` or `pnpm install react` or `bun install react` or `yarn install react` depending on the runtime of your project.
  - Running `ni` will install all packages in your `package.json` file.

# License

MIT
