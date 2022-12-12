A databases inegration  with intuitive data model, automated migrations, type-safety & auto-completion. Work perferly witj nextjs but not only.

- [Webpage](https://www.prisma.io/)
- [Documentation](https://www.prisma.io/docs/reference/api-reference/prisma-client-reference)

## Installation:
```bash
npm install prisma --save-dev
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

    console.log(process.cwd());

    return `${process.cwd()}\\prisma\\files\\${fileName}`;

};

  

if (process.env.NODE_ENV !== "production") global.prisma = prisma;
```