# Amadeus Hotel API MCP Server

This Model Context Protocol (MCP) server provides a bridge to Amadeus Hotel APIs, allowing AI assistants to search for and book hotels through the Amadeus Travel API.

## Features

- Search for hotels in a specific city
- Get detailed hotel offers with pricing and availability
- View specific hotel offer details
- Book hotel rooms with guest and payment information

## Setup

Set the required environment variables before running the server:

```sh
export AMADEUS_API_KEY=your_amadeus_api_key
export AMADEUS_API_SECRET=your_amadeus_api_secret
```

## Available Tools

### Hotel List Tool
- **Name**: `amadeus_hotel_list`
- **Description**: Search for hotels in a specific city with optional filters (amenities, star rating, hotel name)
- **Example**: `amadeus_hotel_list({"cityCode": "PAR", "ratings": [4, 5]})`

### Hotel Search Tool
- **Name**: `amadeus_hotel_search`
- **Description**: Search for hotel offers with pricing for specific dates
- **Example**: `amadeus_hotel_search({"cityCode": "PAR", "checkInDate": "2025-04-01", "checkOutDate": "2025-04-05", "adults": 2})`

### Hotel Offer Tool
- **Name**: `amadeus_hotel_offer`
- **Description**: Get detailed information about a specific hotel offer
- **Example**: `amadeus_hotel_offer({"offerId": "XYZ123"})`

### Hotel Booking Tool
- **Name**: `amadeus_hotel_booking`
- **Description**: Book a hotel offer for specified guests
- **Example**: 
```
amadeus_hotel_booking({
  "offerId": "XYZ123",
  "guests": [
    {
      "name": {
        "title": "MR",
        "firstName": "John",
        "lastName": "Doe"
      },
      "contact": {
        "email": "john.doe@example.com",
        "phone": "+1234567890"
      }
    }
  ],
  "payments": [
    {
      "method": "CREDIT_CARD",
      "card": {
        "vendorCode": "VI",
        "cardNumber": "4111111111111111",
        "expiryDate": "2025-12"
      }
    }
  ]
})
```

## Usage

### Building and Running

```sh
npm install
npm run build
node dist/index.js
```

### Integration with Claude Desktop

To use this MCP server with Claude Desktop, update your configuration file:

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "amadeus-hotel": {
      "command": "node",
      "args": ["/path/to/amadeus-travel/dist/index.js"],
      "env": {
        "AMADEUS_API_KEY": "your_amadeus_api_key",
        "AMADEUS_API_SECRET": "your_amadeus_api_secret"
      }
    }
  }
}
```

## API Documentation

This server integrates with the following Amadeus APIs:

- Hotel List API (`/v1/reference-data/locations/hotels`) - For listing hotels in a location
- Hotel Search API (`/v2/shopping/hotel-offers`) - For finding hotel availability and pricing
- Hotel Offer API (`/v2/shopping/hotel-offers/{offerId}`) - For getting details about a specific offer
- Hotel Booking API (`/v1/booking/hotel-bookings`) - For booking hotel rooms

For more information, refer to the [Amadeus API documentation](https://developers.amadeus.com/self-service/category/hotel).