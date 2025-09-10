# My turborepo - A Production-Ready Monorepo Starter

This repository is a powerful starter kit designed to help you quickly set up a scalable, production-ready monorepo with modern technologies. It solves the initial boilerplate and configuration hell, allowing you to focus on building features.

During my work on this project, I will probably add more notes and thoughts here: [NOTES.md](./NOTES.md).

## ✨ Features

- **Monorepo Powered by Turborepo:** Manage multiple applications and shared packages with ease.
- **Full-Stack TypeScript:** End-to-end type safety across the entire stack.
- **Modern Frontend:** A sleek **Next.js** application with **Tailwind CSS** and **shadcn/ui**.
- **Centralized Database Layer:** A shared `database` package using **Prisma** for clean, type-safe database access.
- **Containerized:** Fully configured with **Docker** and `docker-compose.yml` for easy, reproducible local development and production deployment.

## 📦 What's Inside?

This turborepo includes the following packages and apps:

- `apps/web`: a **Next.js** frontend application.
- `packages/database`: a shared **Prisma** package for database schemas and client.
- `nginx`: a pre-configured **Nginx** reverse proxy to act as an API Gateway.
- `packages/eslint-config`: shared ESLint configurations.
- `packages/typescript-config`: shared `tsconfig.json`s.

## 🚀 Getting Started

**1. Clone the repository:**

```bash
git clone https://github.com/DrArzter/my-turborepo
cd my-turborepo
```

**2. Install dependencies:**
This project uses `pnpm` as a package manager.

```bash
pnpm install
```

**3. Set up the database:**
The project is configured to work with PostgreSQL via Docker.

```bash
docker-compose up -d
```

This will start the PostgreSQL database in the background.

**4. Apply database migrations:**
Navigate to the database package and apply the schema to your newly created database.

````bash
cd packages/database
pnpm prisma migrate dev```

**5. Start the development servers:**
Go back to the root and run the development command.
```bash
cd ../..
pnpm dev
````

This will start all applications in development mode simultaneously.

## 🛠️ Extending the Project

This starter is designed to be easily extensible.

### Adding a New Service

To add a new service (e.g., another Nest.js app), navigate to the `apps` directory and use the framework's CLI:

```bash
cd apps
nest new my-new-service
```

Remember to add a `"dev"` script to its `package.json` so Turborepo can run it.

### Adding a New Package

To add a new shared internal package (e.g., a common `utils` library), follow the official [Turborepo documentation](https://turborepo.com/docs/crafting-your-repository/creating-an-internal-package).

### Containerizing a New Service

To containerize a new service:
<<<<<<< HEAD

1.  Create a `Dockerfile` for it. You can use the examples in the `dockerfiles` directory.
2.  Add the new service to the main `docker-compose.yml` file, defining its build context and dependencies.

## 🤝 Contributing

This project is a living document, and I believe in the power of collective knowledge. If you see a better way to do something, find a bug, or have an idea for an improvement, please feel free to:

- Open an Issue to discuss it.
- Submit a Pull Request with your changes.
- Contact me directly on [Discord (`DrArzter`)](https://discord.com/users/DrArzter), [Telegram](https://t.me/DrArzter), or [email](mailto:chapegarostislav@gmail.com).

I would be happy to learn from you.

## 📜 License

This project is licensed under the **MIT License**. See the [LICENSE.md](./LICENSE.md) file for details.

**TL;DR:** You can do whatever you want with this. I'd be grateful if you give me credit by linking back to this repository.

## 🏛️ Architecture Notes

This project is intentionally designed with a scalable, production-ready architecture in mind, even for this simple starter.

**Nginx as a Reverse Proxy:**
The entire application runs behind an **Nginx reverse proxy**. After running `docker-compose up -d`, the project will be available at `http://localhost:8080`.

**Why?**
This setup provides a single entry point and prepares the project for future expansion. If you want to add more backend microservices (e.g., in Nest.js or Go), you simply need to add them to the `docker-compose.yml` and update the `nginx.conf` file to route traffic accordingly.

---

=======

1.  Create a `Dockerfile` for it. You can use the examples in the `dockerfiles` directory.
2.  Add the new service to the main `docker-compose.yml` file, defining its build context and dependencies.

## 🏗️ Project Structure

```markdown
my-turborepo/
├── apps/                   # Applications
│   └── web/                # Next.js frontend
│
├── packages/               # Shared internal packages
│   ├── database/           # Prisma schemas + client
│   ├── eslint-config/      # Shared ESLint config
│   └── typescript-config/  # Shared TS configs
│
├── nginx/                  # Nginx reverse proxy
│   └── nginx.conf
│
├── docker-compose.yml      # Orchestration for services
├── package.json
├── turbo.json              # Turborepo config
└── README.md
```

## 🤝 Contributing

This project is a living document, and I believe in the power of collective knowledge. If you see a better way to do something, find a bug, or have an idea for an improvement, please feel free to:

- Open an Issue to discuss it.
- Submit a Pull Request with your changes.
- Contact me directly on [Discord (`DrArzter`)](https://discord.com/users/DrArzter), [Telegram](https://t.me/DrArzter), or [email](mailto:chapegarostislav@gmail.com).

I would be happy to learn from you.

## 📜 License

This project is licensed under the **MIT License**. See the [LICENSE.md](./LICENSE.md) file for details.

**TL;DR:** You can do whatever you want with this. I'd be grateful if you give me credit by linking back to this repository.

## 🏛️ Architecture Notes

This project is intentionally designed with a scalable, production-ready architecture in mind, even for this simple starter.

**Nginx as a Reverse Proxy:**
The entire application runs behind an **Nginx reverse proxy**. After running `docker-compose up -d`, the project will be available at `http://localhost:8080`.

**Why?**
This setup provides a single entry point and prepares the project for future expansion. If you want to add more backend microservices (e.g., in Nest.js or Go), you simply need to add them to the `docker-compose.yml` and update the `nginx.conf` file to route traffic accordingly.

---

>>>>>>> f1e34c0 (Update readme for the new version)
For now this project is maintaned by [me](https://github.com/DrArzter).
