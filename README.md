# Stripe Issuing and Treasury: An Embedded Finance starter application

This sample demonstrates a basic web application with embedded finance features built on Stripe’s Issuing and Treasury APIs.

<p align="center">
  <img width="715" alt="Issuing and Treasury sample app card details screenshot" src="https://github.com/stripe-samples/issuing-treasury/assets/103917180/5acecf09-d65d-499c-9171-eb187656dd2b" />
</p>

## Demo

See the sample app live at <https://baas.stripe.dev>

If you choose not to skip onboarding with prefilled info, then follow these steps when redirected to the Stripe Connect Onboarding form:

- Enter “000 000 0000” for phone number and any fake email address
- Click “Use test code” when prompted for SMS verification
- Click “Skip this step” when prompted to verify your identity

## Features

- Onboard and verify business customers 🔍
- Issue cards 💳
- Display full card numbers with PCI compliance 🔢
- Create financial accounts 🏦
- Simulate test payments ⚡
- Review transactions 📃

For details of more features see the [Issuing and Treasury sample app documentation](https://stripe.com/docs/baas/start-integration/sample-app).

## Prerequisites

- Activate Stripe Issuing and Treasury in test mode through this link: <https://dashboard.stripe.com/setup/treasury/activate?a=1>
- Obtain your Stripe API keys at <https://dashboard.stripe.com/test/apikeys>

## Deploy the web application on Render

You can immediately deploy this sample app to a unique, public URL (for example: `https://issuing-treasury-xyz1.onrender.com`) with no coding required by using Render.

Click the button below to get started:

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://stripe.com/docs/baas/start-integration/sample-app?ui=copy-sample-app&copy-sample-app-tabs=no-code-deployment#choose-how-to-deploy-the-app)

## Local development

You can also clone this repo and run it locally by following the steps below.

### Clone the repo

Clone this repo and then run these steps inside it.

    git clone https://github.com/stripe-samples/issuing-treasury.git && cd issuing-treasury

### Node.js installation

Install the required Node.js runtime. You can install it directly from the [Node.js website](https://nodejs.org/en/download/releases)
but we recommend using a Node version manager. Most version managers can read the required version off of `.node-version`
and install it.

If you're using the `nodenv` Node version manager ([setup instructions for nodenv](https://github.com/nodenv/nodenv#installation)), use:

    nodenv install

If you're using the popular `nvm` Node version manager ([setup instructions for Node Version Manager](https://github.com/nvm-sh/nvm#installing-and-updating)), use:

    nvm install

### Dependency installation

Once Node.js is installed and activated, install the application's dependencies using:

    npm install

### Environment variables file setup

Replicate `.env.example` as `.env` using:

    cp .env.example .env

Update `.env` to reflect:

- **NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY**: Your Stripe publishable test mode [API key](https://dashboard.stripe.com/test/apikeys) (starts with `pk_test_...`).
- **STRIPE_SECRET_KEY**: Your Stripe secret test mode [API key](https://dashboard.stripe.com/test/apikeys) (starts with `sk_test_...`).
- **NEXTAUTH_SECRET**: For JWT encryption by NextAuth.js ([learn more](https://next-auth.js.org/configuration/options#nextauth_secret)). Use `openssl rand -base64 32` to obtain a new one.
- **NEXTAUTH_URL**: Your application URL, for local use you can keep the default "<http://localhost:3000>".
- **CONNECT_ONBOARDING_REDIRECT_URL**: Your application URL, for local use you can keep the default "<http://localhost:3000>".

### Database setup

On Mac, follow these instructions to install Postgres:

    brew install postgresql@14
    createuser -s postgres

You'll find more about the why you need the `createuser` step [here](https://stackoverflow.com/a/15309551).

Next, create the database with:

    npx prisma db push

If it errors out (perhaps due to permission issue running the Prisma CLI), simply run the included script:

    ./db/setup-database.postgres.sh

This script creates a local Postgres `issuing_treasury` database.

** notes ** The db script didn't work. 
```
kater:~/src/issuing-treasury (main) 11:38  $ brew services restart postgresql@14
Stopping `postgresql@14`... (might take a while)
==> Successfully stopped `postgresql@14` (label: homebrew.mxcl.postgresql@14)
==> Successfully started `postgresql@14` (label: homebrew.mxcl.postgresql@14)
kater:~/src/issuing-treasury (main) 11:38  $ brew link postgresql@14 --force
Warning: Already linked: /opt/homebrew/Cellar/postgresql@14/14.9
To relink, run:
  brew unlink postgresql@14 && brew link postgresql@14
kater:~/src/issuing-treasury (main) 11:39  $ brew services info --all
postgresql@14 (homebrew.mxcl.postgresql@14)
Running: ✔
Loaded: ✔
Schedulable: ✘
User: kater
PID: 71754
kater:~/src/issuing-treasury (main) 11:39  $ lsof -P -sTCP:LISTEN -i TCP -a -p 71754
COMMAND    PID  USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
postgres 71754 kater    7u  IPv6 0xc3eb81b4876b9731      0t0  TCP localhost:5432 (LISTEN)
postgres 71754 kater    8u  IPv4 0xc3eb81b967c66f29      0t0  TCP localhost:5432 (LISTEN)
kater:~/src/issuing-treasury (main) 11:39  $ ./db/setup-database.postgres.sh
psql: error: connection to server on socket "/tmp/.s.PGSQL.5432" failed: FATAL:  database "kater" does not exist

Creating database...
psql: error: connection to server on socket "/tmp/.s.PGSQL.5432" failed: FATAL:  database "kater" does not exist
Creating users table...
psql: error: connection to server on socket "/tmp/.s.PGSQL.5432" failed: FATAL:  database "issuing_treasury" does not exist
Setup complete!
```


### Application launch

After necessary setups, launch the application with `npm run dev`.

*Note: This application serves as an example and should not proceed to production deployment as it is.*

## Customizing your UI with the Devias Material UI theme

This sample uses the [free Devias UI kit](https://github.com/devias-io/material-kit-react) under an MIT license, which seamlessly integrates with Material UI and React.

You can easily customize aspects of the theme like the color palette by modifying the code in `/src/theme`.

To build a full-featured, production-ready application we recommend the [Devias Pro](https://material-kit-pro-react.devias.io/) version, which offers additional layouts, advanced React components, pre-built dashboards, and essential TypeScript support that ensures your code remains clean, robust, and scalable.
