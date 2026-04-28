# Card Validator

A modern, minimal card validation frontend that integrates with a backend API to validate credit card numbers in real-time.

## Features

- **Real-time Card Formatting** — Automatically formats input with spaces every 4 digits (e.g., `1234 5678 9012 3456`)
- **Loading State** — Displays an animated spinner during validation (minimum 1.5 seconds for better UX)
- **Dynamic Messages** — Displays API-provided validation messages with status-based colors
  - Green for valid cards
  - Red for invalid cards
- **Error Handling** — Comprehensive error handling for network issues:
  - Connection failures: "Unable to reach the server. Please check your connection."
  - Timeouts (30s): "Request timed out. The server may be waking up — please try again."
- **Keyboard Support** — Press Enter to validate immediately
- **Responsive Design** — Beautiful dark theme with glassmorphic effects
- **Interactive API Docs Link** — Quick access to API documentation in the top-right corner

## Project Structure

```
card-validation-frontend/
├── index.html          # Main HTML file with embedded CSS and JavaScript
└── README.md           # This file
```

## Getting Started

### Prerequisites

- Any modern web browser (Chrome, Firefox, Safari, Edge)
- Backend API running at `https://card-validation-api-j5eq.onrender.com`

### Setup

1. Clone or download this repository
2. Open `index.html` in your browser
3. Ensure the backend API is running and accessible at `https://card-validation-api-j5eq.onrender.com`

## Usage

1. Enter a card number in the input field (spaces are automatically added)
2. Click the "Validate" button or press Enter
3. The form will show a loading state while the request is in flight
4. View the validation result:
   - **Green checkmark** if the card is valid
   - **Red X** if the card is invalid
5. Both states display the message from the API response

## API Integration

### Endpoint

```
POST https://card-validation-api-j5eq.onrender.com/api/validate-card
```

### Request Format

```json
{
  "cardNumber": "1234567890123456"
}
```

### Response Format

**Success (200):**
```json
{
  "valid": true,
  "message": "This card number is valid"
}
```

**Failure (400 or 200):**
```json
{
  "valid": false,
  "message": "This card number is not valid"
}
```

The `message` field is optional. If not provided, default messages are used.

## Frontend Validation

Before sending to the API, the frontend validates that:
- Card number is not empty
- Card number contains only numeric characters

## Features in Detail

### Loading State
- Button displays an animated spinner
- Button is disabled during the request
- Minimum loading time of 1.5 seconds ensures a smooth UX experience

### Error Handling
- **Network Errors** — Detected via TypeError or offline status
- **Timeout Errors** — Aborts after 30 seconds with a specific message
- **Other Errors** — Generic fallback message

### Input Formatting
- Numbers are automatically formatted with spaces: `1234 5678 9012 3456`
- Non-numeric characters are rejected
- Spaces are stripped before sending to the API

## Styling

The design uses:
- **Dark Theme** — Modern, minimal aesthetic
- **Glassmorphism** — Subtle blur and transparency effects
- **Smooth Transitions** — All interactions are animated
- **Custom Tailwind Configuration** — Extended colors and spacing from the design system

## Browser Compatibility

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## Development

### Modifying the API Endpoint

Change the fetch URL in the JavaScript section:
```javascript
const response = await fetch('https://card-validation-api-j5eq.onrender.com'
```

### Adjusting Minimum Loading Time

Change the timeout value (in milliseconds):
```javascript
const minLoadingDelay = new Promise(resolve => setTimeout(resolve, 1500)); // 1500ms
```

### Adjusting Request Timeout

Change the AbortController timeout (in milliseconds):
```javascript
const timeoutId = setTimeout(() => controller.abort(), 30000); // 30000ms = 30 seconds
```


