This project uses a custom setup for handling different environments (development, test, and production) with Next.js, avoiding the default behavior where Next.js always uses the .env.production file during builds.

Environment Setup
To manage environment-specific configurations, we renamed the environment files and used the env-cmd library.

Steps to Set Up Environments
Rename Environment Files
Rename your environment files to custom names so Next.js does not pick them up automatically. Use the following names:

```
.env.development → .env.dev
.env.test → .env.test
.env.production → .env.prod
Install env-cmd
```
To use these custom environment files during builds, install env-cmd:

bash
Copy code
```
npm install env-cmd
```
Update package.json Scripts
Modify the scripts in package.json to specify the correct environment file for each environment:

json
Copy code

```
"scripts": {
  "dev": "env-cmd -f .env.dev next dev --port 5000",
  "build:dev": "env-cmd -f .env.dev next build",
  "build:test": "env-cmd -f .env.test next build",
  "build:prod": "env-cmd -f .env.prod next build",
  "start:dev": "env-cmd -f .env.dev next start --port 5000",
  "start:test": "env-cmd -f .env.test next start --port 5000",
  "start:prod": "env-cmd -f .env.prod next start --port 3000",
  "test": "rimraf .next && npm run build:test && npm run start:test",
  "prod": "rimraf .next && npm run build:prod && npm run start:prod",
  "lint": "next lint"
}
```
.gitignore Configuration
To prevent environment files from being pushed to GitHub, add them to your .gitignore file:

plaintext
Copy code
# Ignore environment files
.env*
This setup ensures each environment uses its dedicated configuration file without accidental exposure of sensitive information.
