# Shopify App with Remix and AWS EventBridge Integration

This project is a Shopify app built with the Remix framework and TypeScript. The app integrates with AWS EventBridge to handle Shopify events using a custom event bus.

## Prerequisites

Before you start, make sure you have:

- Node.js and npm installed on your machine
- A [Shopify Partner account](https://partners.shopify.com/) set up with an app
- Access to AWS to configure EventBridge

## Project Setup

### Step 1: Initialize the Shopify App

To create your Shopify app using the Shopify CLI, run the following command:

```bash
npm init @shopify/app
```

Follow the CLI prompts to set up the project:

- **Project Name**: Choose a name for your project.
- **Framework**: Select `remix-app`.
- **Language**: Choose `typescript`.
- **Use experimental features**: Select `Yes`.

### Step 2: Navigate to the Project

Once the project is created, navigate to your project directory:

```bash
cd your-project-name
```

### Step 3: Run the Development Server

Start the development server using:

```bash
npm run dev
```

You should now be able to view the app in your local development environment.

### Step 4: Configure Shopify and AWS EventBridge

#### Shopify Partner Dashboard

1. Go to the [Shopify Partner Dashboard](https://partners.shopify.com/) and select your app.
2. In the **Apps** section, click on your app to view its configuration.
3. Scroll down to **Amazon EventBridge** and click on **Create Event Bus**.
4. Follow the instructions to create an event bus on Shopify and confirm the event bus on AWS.

#### AWS EventBridge Setup

1. Go to your AWS Console and navigate to **EventBridge**.
2. Create a new rule by selecting **Create Rule**.
3. Set a name for the rule.
4. Choose the correct event bus created earlier.
5. Scroll down to the **Event Pattern** section:
   - Change **Event Source** to `EventBridgePartners`.
   - Set the partner to `shopify`.
   - Select **All Events** to capture all event types from Shopify.

#### Retrieve Event Bus ARN

1. Go to **Partner Event Source** in AWS and click on the event bus created for Shopify.
2. Copy the **ARN** of the event bus.

### Step 5: Update `shopify.server.toml` Configuration

1. In your project directory, locate the `shopify.server.toml` file under the `webhooks` section.
2. Under the specified webhook topic, update the `uri` field with the ARN value you copied from AWS:

```toml
[[webhooks]]
topic = "YOUR_TOPIC_NAME"
address = "arn:aws:events:YOUR_AWS_REGION:YOUR_ACCOUNT_ID:event-bus/YOUR_EVENT_BUS_NAME"
```

Make sure to replace `YOUR_TOPIC_NAME`, `YOUR_AWS_REGION`, `YOUR_ACCOUNT_ID`, and `YOUR_EVENT_BUS_NAME` with the appropriate values.

## Running the App

After completing these steps, your Shopify app should be set up to receive events from Shopify via AWS EventBridge. You can start receiving and processing events based on the rules and patterns you've configured.

To run the app in development mode:

```bash
npm run dev
```

## Additional Resources

- [Shopify App CLI Documentation](https://shopify.dev/docs/apps/tools/cli)
- [AWS EventBridge Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html)

## License

This project is licensed under the MIT License.
