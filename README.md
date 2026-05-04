# Documantions-for-everything

# Backend NestJs + Prisma

## Használd a következő [linket](https://github.com/hgabor/nestjs-keret-2025)

Töltsd le majd miután kicsomagoltad és Visual Studio Code-dal elindítottad add ki az alábbi parancsokat a terminálban:

```
npm i
npx prisma generate
```

Ez után ha szükséges hogy az adatbázist lekérd prisma formában akkor add ki az alábbi parancsot miután beállítottad az .env fájlt.

```
npx prisma db pull
```

Ezek után ha kell modosíts a modellen ha kell vagy adj hozzá új táblát. Esetleg akár kapcsolatot is az alábbi módon.

```
model basics{
    id      Int     @id @default(autoincrement())
    connectingTobasic connectingTobasics[]
}

model connectingTobasics{
    id      Int     @id @default(autoincrement())
    //itt adjuk meg hogy mi alapján kapcsolodjanak
    basic basics @relation(fields: [basic_id], references: [id])
    //a két összekapcsolodó elemnek ugyan olyan elemnek kell lennie
    basic_id        Int
}
```

Ha ezek megvannak jöhet ez után a seed-elés ha kötelező

```
import dotenv from 'dotenv';
dotenv.config();

//ez ahoz szökséges hogy tudjunk elemeket létrehozni
import { PrismaClient } from '../generated/prisma/client';

const prisma = new PrismaClient();

async function itemfiller() {
    await prisma.{/*bármilyen prisma model*/}.create({
      data:{
        //ide kerülnek az elemek értékének megadása
      }
    })


    //ez nem kötelező de legalább jelzi hogy lefutott minden
    console.log("Seeding done")
}


//ezzel a résszel indul el az elözöleg megírt kód és hozunk létre elemeket az adatbázisban
itemfiller()
  .then(async () => {
    await prisma.$disconnect();
  })
  .catch(async (e) => {
    console.error(e);
    await prisma.$disconnect();
    process.exit(1);
  });
```

