A databases inegration  with intuitive data model, automated migrations, type-safety & auto-completion. Work perferly witj nextjs but not only.

- [Website](https://www.prisma.io/)
- [Documentation](https://www.prisma.io/docs/reference/api-reference/prisma-client-reference)

## Installation:
```bash
npm install prisma --save-dev
```


## Eviroments
During development and small production sqlite can be used as a database, after the migration it's done by prisma
```prisma
datasource db {
    provider = "sqlite"
    url      = env("DATABASE_URL")
}
```
Into the `.env` file add
```env
DATABASE_URL="file:database.db"
```


## Npm commands
Add the follwing in `package.json` to add npm scripts
```json
"prisma": "npx prisma studio",
"db": "npx prisma db push"
```

After `schema.prisma` has been modifed, run the folling to update the database:
```bash
npm run db
```

Open prisma studio to see in real time changes into the databases
```bash
npm run prisma
```


## Prisma client 
Add the following script in a `prisma.js` file in the `prisma` folder, then import the client in the entire app from it. This prevent to create multiple instances of the database during development (save to refersh)
```js
import { PrismaClient } from "@prisma/client";

export const prisma = global.prisma || new PrismaClient();
export const filePath = (fileName) => {
    return `${process.cwd()}\\prisma\\files\\${fileName}`;
};

if (process.env.NODE_ENV !== "production") global.prisma = prisma;
```