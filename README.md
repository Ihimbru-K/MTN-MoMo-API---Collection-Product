# MoMo API Node.js Server-side for the Collection Product

## Introduction.

This server application is designed to interact with the MoMo (Mobile Money) API provided by MTN for the collection product service. It offers various endpoints to handle API user creation, user retrieval, API key retrieval, MoMo token generation, and payment requests. Additionally, there is a simple front-end for initiating payment requests.

## Server-Side

#### Setup

Before running the server, ensure the following steps are completed:

1. Install Node.js and npm.
2. Clone the repository to your local machine.
3. Navigate to the project directory and run `npm install` to install dependencies.
4. Set up environment variables in a `.env` file for `MOMO_SUBSCRIPTION_KEY`.

#### Endpoints and Their Functionalities

##### 1. Default Route (`GET /`)

A basic route to check if the API is running. Returns a simple "Hello World!" message.

##### 2. Create API User (`POST /create-api-user`)

Creates an API user on the MoMo platform. This endpoint generates a unique user ID (`X-Reference-Id`) which is used in subsequent requests. It expects a callback URL in the request body.

**Dependencies**: None.

**Response**: Returns the created user's ID and the response from the MoMo API.

##### 3. Get Created User (`GET /get-created-user/:userId`)

Retrieves details of a created API user using the user ID. This route is essential to verify that a user exists on the MoMo platform.

**Dependencies**: Requires a user ID generated by `/create-api-user`.

##### 4. Retrieve API Key (`POST /retrieve-api-key/:userId`)

Retrieves the API key for a given user ID. This API key is necessary for generating a MoMo token and should be securely stored on the client side.

**Dependencies**: Requires a user ID generated by `/create-api-user`.

##### 5. Generate MoMo Token (`POST /generate-api-token`)

Fetches a MoMo token using the user ID and API key. This token is crucial for making payment requests and should be securely stored on the client side.

**Request Example**:

```json
{
  "userId": "generated-user-id",
  "apiKey": "retrieved-api-key"
}
```

**Dependencies**:

- Requires a user ID generated by `/create-api-user`.
- Requires an API key retrieved by `/retrieve-api-key/:userId`.

##### 6. Request to Pay (`POST /request-to-pay`)

Sends a payment request to the MoMo API. This endpoint requires the total amount, the payer's phone number, and the MoMo token ID.

**Request Example**:

```json
{
  "total": "amount",
  "phone": "payer-phone-number",
  "momoTokenId": "momo-token"
}
```

**Dependencies**: Requires a MoMo token generated by `/generate-api-token`.

#### Running the Server

To start the server, run `npm start` or `node <server-file-name>.js` in the terminal. The server will listen on the port defined in the server file (default is 3001).

### Environment

The server and all endpoints are configured to run in the MoMo API sandbox environment. This is a test environment provided by MTN for development and testing purposes. It simulates the MoMo API's behavior without affecting live data or incurring actual transactions.

**Note**: The sandbox environment is for testing only. To move to production, you will need to configure the endpoints with production URLs and obtain production credentials.

## Front-End

The front-end is a simple HTML/CSS/JavaScript application for testing the payment process. It allows users to input the phone number and amount, then handles the full process: API user creation, user retrieval, API key retrieval, MoMo token generation, and finally, making the payment request.

### Running the Front-end

To run the front-end effectively:

1. Use a local server to serve the front-end files. This can be done using tools like the Live Server extension in Visual Studio Code, which will also provide the benefit of auto-reloading the page on changes.
2. Open the `index.html` file through the live server.
3. Enter the phone number and amount in the provided fields.
4. Click the 'Pay Now' button to initiate the payment process.

**Note**: Running the front-end directly in a browser may not work due to security restrictions like the Same-Origin Policy. It's recommended to use a local server setup for proper functionality.

### Front-end Files

- `index.html`: The HTML file for the user interface.
- `style.css`: The CSS file for styling the front-end.
- `script.js`: The JavaScript file that handles the interaction with the Node.js server and the MoMo API.
