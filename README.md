# Create T3 App

This is an app bootstrapped according to the [init.tips](https://init.tips) stack, also known as the T3-Stack.

## t3-chat-app

This app is from a youtube tutorial created by TomDoesTech: https://youtu.be/dXRRY37MPuk
gihub repo: https://github.com/TomDoesTech/t3-chat

### Slight changes

create-t3-app has made changes to their template that cause the original tutorial code to throw an error when trying to start your web socket server.
This error occurs because in the tutorial version of create-t3-app template the ./src/server/env.mjs and ./src/serve/env-schema.mjs files were .js files.
We cannot simply change the file type to .js because in the template nextjs requires the files to be .mjs files for it to import them to the /next.config.mjs file.
The work around I found was to add "moduleResolution": "node16" to ./tsconfig-server.json and then in ./src/server/db/client.ts remove <code>import { env } from "../env";</code> and instead use a dynamic import like <code>(async () => {
      const { env } = await import("../env.mjs");
    })().catch(err => console.error(err))</code>
    
    
This should fix the error when starting the web socket server.
