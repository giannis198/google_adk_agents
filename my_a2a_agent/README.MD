
# A2A (Agent-to-Agent) Hello World Example

This project demonstrates the Agent-to-Agent (A2A) communication protocol using Google ADK (Agent Development Kit). It showcases how to create and connect remote agents that can communicate with each other seamlessly.

## Overview

This example consists of two main components:

1. **Product Catalog Agent** - An external vendor's product catalog service that provides product information via A2A protocol
2. **Customer Support Agent** - A customer support assistant that connects to the remote Product Catalog Agent to provide product information to customers

The A2A protocol enables secure and standardized communication between agents, allowing them to share tools and capabilities across different systems.

## Architecture

```
Customer Support Agent (Local)
    ↓
RemoteA2aAgent (Proxy)
    ↓
A2A Protocol
    ↓
Product Catalog Agent (Remote - port 8002)
```

## Features

- **Remote Agent Integration**: Demonstrates how to connect to remote agents using the A2A protocol
- **Tool Sharing**: Remote agents can expose their tools to be used by other agents
- **Agent Cards**: Uses standardized agent card metadata for service discovery
- **Error Handling**: Includes retry logic with configurable parameters
- **Product Lookup**: Built-in product catalog with mock data for demonstration

## Setup

1. **Create and Activate Virtual Environment**:
   ```bash
   # Create a virtual environment
   python -m venv venv

   # Activate the virtual environment
   # On Linux/Mac:
   source venv/bin/activate
   # On Windows:
   venv\Scripts\activate
   ```

2. **Install Dependencies**:
   ```bash
   pip install -r ../requirements.txt
   # or install directly:
   pip install google-adk python-dotenv uvicorn fastapi
   ```

3. **Set up Environment Variables**:
   Create a `.env` file in the project root with your Google API configuration:
   ```env
   GOOGLE_API_KEY=your_api_key_here
   ```

## Usage

The application requires two processes to run:

### 1. Start the Remote Product Catalog Agent
Run this command from the project root:
```bash
uvicorn my_a2a_agent.remote_a2a.hello_world.agent:a2a_app --host localhost --port 8002
```

This will start the remote agent server on port 8002, exposing the product catalog functionality through the A2A protocol.

### 2. Start the Customer Support Agent
In a separate terminal, run the customer support agent:
```bash

adk run my_a2a_agent or adk web

```

## Project Structure

- `agent.py` - Contains the Product Catalog Agent implementation with mock product data
- `README.MD` - This documentation file
- `.env` - Environment variables (not included in version control)

## Product Catalog Data

The demo includes the following sample products:
- iPhone 15 Pro
- Samsung Galaxy S24
- Dell XPS 15
- MacBook Pro 14
- Sony WH-1000XM5 Headphones
- iPad Air
- LG Ultrawide 34 Monitor

## How It Works

1. The Product Catalog Agent runs as a remote service on port 8002
2. The Customer Support Agent creates a RemoteA2aAgent proxy that connects to the remote agent
3. When a customer asks about a product, the Customer Support Agent uses the remote agent's tools via A2A protocol
4. The remote agent provides product information which is then formatted and presented to the customer

## A2A Protocol Benefits

- **Interoperability**: Agents from different systems can work together
- **Security**: Standardized authentication and communication protocols
- **Scalability**: Distributed agent architecture
- **Flexibility**: Easy integration with external services

## Troubleshooting

- Make sure port 8002 is available before starting the remote agent
- Ensure your API keys are properly configured in the `.env` file
- Verify that the agent card endpoint is accessible at `http://localhost:8002/.well-known/agent` when the server is running

## Next Steps

- Integrate with real product databases
- Add authentication and authorization
- Implement additional agent services
- Explore multi-agent collaboration patterns

## Testing the Agent

Here are some sample queries you can try with the Customer Support Agent to test the A2A communication:

1. "What smartphones do you have in your catalog?"
2. "Show me the price of iPhone 15 Pro"
3. "What are the specifications for the Samsung Galaxy S24?"
4. "Do you have any laptops available?"
5. "Compare the MacBook Pro 14 and Dell XPS 15"
6. "What headphones do you sell?"
7. "Show me all products from your catalog"
8. "What is the price of the LG Ultrawide 34 Monitor?"
9. "Tell me about the iPad Air"
10. "Find products under $1000"

These queries will test the connection between the Customer Support Agent and the Product Catalog Agent, demonstrating the A2A communication protocol in action.
