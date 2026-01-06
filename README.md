# fastify-typeorm-postgres
- Create Node project
    1. Create empty repo in Github and clone to computer
    2. Run `npm init -y` (creates package.json with default setting)
    3. Install dependencies `npm i fastify` (or any other libraries wanted)
    4. Install dev dependencies
       - `npm i -D nodemon typescript @types/node ts-node @tsconfig/node22` (this will continuously run server on changes automatically)

5. Create tsconfig.json file with default values https://github.com/tsconfig/bases#node-14-tsconfigjson (change depending on node version)
```bash
    {
      "$schema": "https://json.schemastore.org/tsconfig",
      "display": "Node 22",
      "_version": "22.0.0",
        
      "compilerOptions": {
        "lib": ["es2023"],
        "module": "nodenext",
        "target": "es2022",
        "outDir": "build",   # Specifys an output folder for all .js files.
        "strict": true,
        "esModuleInterop": true,
        "skipLibCheck": true,
        "moduleResolution": "node16"
      }
    }
```

6. Update .gitignore file
```bash
build
.idea
```
   
7. Create index.ts file
```ts
import fastify from 'fastify'

const server = fastify()

server.get('/ping', async (request, reply) => {
  return 'pong\n'
})

server.listen({ port: 8080 }, (err, address) => {
  if (err) {
    console.error(err)
    process.exit(1)
  }
  console.log(`Server listening at ${address}`)
})
```

8. Build and run app
- Add scripts to package.json
```bash
{
  "scripts": {
    "build": "tsc -p tsconfig.json",
    "dev": "nodemon index.ts",
    "start": "node build/index.js" # the tsconfig.json puts .js files in the outDir folder which is set to /build
  }
}
```
- Run `npm run build` // this will compile index.ts into index.js which can be executed using Node.js
- Run dev for live reloading with nodemon `npm run dev`