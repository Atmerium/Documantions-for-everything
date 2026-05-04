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