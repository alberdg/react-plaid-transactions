# React Plaid Transactions

## Motivation

The idea is to be able to fetch user bank transactions using Plaid api https://plaid.com/docs/api/
The user will be presented with an initial screen where he/she will accept terms and conditions and then go through Plaid screens to provide the open banking data needed.

Once that is done Plaid returns a public token, such token needs to be exchanged with an access token in order to be able to request user transactions.

## Versions

- In a first version the aim is to display the average income and expenses during this year.
- The second version will also display the categories of the most recurring expenses
- The third version will add some charts displaying the income vs expenses per year and per month

## Architecture

### Frontend

The frontend will be developed using ReactJS and Typescript.

- It will use plaid library for all the plaid UI stuff
- It will use axios to communicate with the backend
- It will use cypress for E2E testing

### Backend

The backend must be able to provide functionality to create a plaid link token https://plaid.com/docs/api/tokens/ and also to fetch user transactions. These transactions will not be stored for the sake of the example, they will always be re-fetched.

- It will use AWS CDK as infrastructure as code
- It will create a rest api with 2 endpoints
  - GET /plaid/link-token
  - POST /plaid/transactions
    - The body must be { "publicToken": "Whatever public token received from Plaid" }

## Getting started

- In order to deploy the backend you need to cd to the infra directory and run ./deploy.sh

- Once the AWS deployment is done cd to web directory. You will need to provide the following values in .env file:

REACT_APP_PLAID_CLIENT_ID=
REACT_APP_PLAID_SECRET=
REACT_APP_PLAID_SANDBOX_REDIRECT_URI=http://:3000/oauth
REACT_APP_PLAID_EXAMPLE_API_BASE_URL=

- You are ready to start, from web directory run yarn start
