# cours a rajouter:
pense bete pour lecons a faire 

# PHP
- switch case sur les url
- diagramme de classe (classe abstraite / héritage)
- json_encode
- lecons sur ce code 
================================================================================
<?php

namespace App\Controller;

abstract class AbstractController{

    public function render(string $template, string $title,array $data = []):void{

        include  __DIR__. "/../../templates/template_".$template.".php";

    }

    public function jsonResponse(array $data, int $statusCode = 200):void{
        http_response_code($statusCode);
        echo json_encode($data,JSON_PRETTY_PRINT);
    }

    public function formSubmit(array $post){
        if(isset($post["submit"])){
            return true;
        }
        return false;
    }
}
================================================================================
- fonction implodeR
- la regle du "dry don't repeat yourself" en POO

# Java-Script
# Java



# Nuxt Minimal Starter

Look at the [Nuxt documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Setup

Make sure to install dependencies:

```bash
# npm
npm install

# pnpm
pnpm install

# yarn
yarn install

# bun
bun install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# pnpm
pnpm dev

# yarn
yarn dev

# bun
bun run dev
```

## Production

Build the application for production:

```bash
# npm
npm run build

# pnpm
pnpm build

# yarn
yarn build

# bun
bun run build
```

Locally preview production build:

```bash
# npm
npm run preview

# pnpm
pnpm preview

# yarn
yarn preview

# bun
bun run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
