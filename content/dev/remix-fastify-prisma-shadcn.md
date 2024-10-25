+++
date = "2024-10-23"
title = "remix-fastify-prisma-shadcn setup"
tags = ["remix"]
toc = false
draft = false
+++

### remix

https://remix.run/resources/remix-fastify

```
npx create-remix@latest --template mcansh/remix-fastify/examples/vite
```

### tailwind

https://tailwindcss.com/docs/guides/remix

```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init --ts -p

```

`./tailwind.config.ts`
add content path 
```
content: ['./app/**/*.{js,jsx,ts,tsx}'],
```

```ts
import type { Config } from 'tailwindcss'

export default {
  content: ['./app/**/*.{js,jsx,ts,tsx}'],
  theme: {
    extend: {},
  },
  plugins: [],
} satisfies Config
```

`./app/tailwind.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
`./app/root.tsx
```tsx
import type { LinksFunction } from "@remix-run/node";
import stylesheet from "~/tailwind.css?url";

export const links: LinksFunction = () => [
  { rel: "stylesheet", href: stylesheet },
];
```

check
`./app/routes/_index.tsx`
```tsx
export default function Index() {
  return (
    <h1 className="text-3xl font-bold underline">
      Hello world!
    </h1>
  )
}
```
``
### shadcn ui

https://ui.shadcn.com/docs/installation/remix outdated for the moment 2024.10.24

`tsconfig.json`
add paths alias under compilerOptions
```json
{
  "include": [
    "**/*.ts",
    "**/*.tsx",
    "**/.server/**/*.ts",
    "**/.server/**/*.tsx",
    "**/.client/**/*.ts",
    "**/.client/**/*.tsx"
  ],
  "compilerOptions": {
    "lib": ["DOM", "DOM.Iterable", "ES2022"],
    "types": ["@remix-run/node", "vite/client"],
    "isolatedModules": true,
    "esModuleInterop": true,
    "module": "ESNext",
    "jsx": "react-jsx",
    "moduleResolution": "Bundler",
    "moduleDetection": "force",
    "resolveJsonModule": true,
    "target": "ES2022",
    "skipLibCheck": true,
    "strict": true,
    "allowJs": true,
    "forceConsistentCasingInFileNames": true,
    "baseUrl": ".",
    "paths": {
      "~/*": ["./app/*"],
      "@/*": ["./app/*"]
    },

    // Remix takes care of building everything in `remix build`.
    "noEmit": true
  }
}

```

```
npx shadcn@latest init
```

check

```
npx shadcn@latest add button
```

```tsx
import { Button } from "@/components/ui/button"

export default function Home() {
  return (
    <div>
      <Button>Click me</Button>
    </div>
  )
}

```

### prisma

```
npm install prisma @types/node --save-dev
npx prisma init
```

set .env and add it to your .gitignore

```
DATABASE_URL="postgresql://johndoe:randompassword@localhost:5432/mydb?schema=public"

e.g.
DATABASE_URL="postgresql://jiyu:jiyu@localhost:5432/c0_stack?schema=public"
```

`./prisma/schema.prisma`

```
// This is your Prisma schema file,
// learn more about it in the docs: https://pris.ly/d/prisma-schema

// Looking for ways to speed up your queries, or scale easily with your serverless or edge functions?
// Try Prisma Accelerate: https://pris.ly/cli/accelerate-init

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model Post {
  id        Int      @id @default(autoincrement())
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  title     String   @db.VarChar(255)
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}

model Profile {
  id     Int     @id @default(autoincrement())
  bio    String?
  user   User    @relation(fields: [userId], references: [id])
  userId Int     @unique
}

model User {
  id      Int      @id @default(autoincrement())
  email   String   @unique
  name    String?
  posts   Post[]
  profile Profile?
}
```

```
npx prisma migrate dev --name init

alternative, or to turn db schema into a prisma schema
prisma db pull
```

```
npm install @prisma/client
npx prisma generate
```

`./app/db/dbtest.ts`

```ts
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

async function main() {
  await prisma.user.create({
    data: {
      name: 'Alice',
      email: 'alice@prisma.io',
      posts: {
        create: { title: 'Hello World' },
      },
      profile: {
        create: { bio: 'I like turtles' },
      },
    },
  })

  const allUsers = await prisma.user.findMany({
    include: {
      posts: true,
      profile: true,
    },
  })
  console.dir(allUsers, { depth: null })
}

main()
  .then(async () => {
    await prisma.$disconnect()
  })
  .catch(async (e) => {
    console.error(e)
    await prisma.$disconnect()
    process.exit(1)
  })
```

run 
`npx tsx ./app/db/dbtest.ts` 

expected result

```json
[
  {
    id: 1,
    email: 'alice@prisma.io',
    name: 'Alice',
    posts: [
      {
        id: 1,
        createdAt: 2024-10-24T22:14:46.303Z,
        updatedAt: 2024-10-24T22:14:46.303Z,
        title: 'Hello World',
        content: null,
        published: false,
        authorId: 1
      }
    ],
    profile: { id: 1, bio: 'I like turtles', userId: 1 }
  }
]
```

