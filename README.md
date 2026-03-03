```markdown
# 📈 TikTok Incremental Bot

## Description

This project, internally identified as `hsvob972-eng/3rd_perfect_bot` and externally as "tiktok-incremental-bot", is a Node.js application designed to automate and manage TikTok video interactions, specifically focusing on view monitoring and providing a foundation for incremental view logic. It leverages an Express.js server to expose an API for interacting with TikTok, incorporating features like real-time view checking and an adaptive request system to avoid detection and ensure efficiency.

The core functionality involves scraping TikTok video pages to extract current engagement statistics (views, likes, comments, shares) while employing sophisticated mechanisms such as caching, intelligent rate limiting, and dynamic user-agent rotation. Although the full incremental view logic isn't explicitly detailed in the provided structure, the architecture lays a robust foundation for building a sophisticated and resilient view incrementation bot.

## Features

*   **Express.js API:** Provides a clean and accessible RESTful API for fetching TikTok video statistics.
*   **Real-time TikTok Data Fetching:** Scrapes TikTok video pages to extract current views, likes, comments, and shares.
*   **Intelligent Caching:** Implements a `Map`-based caching mechanism with a configurable duration to reduce redundant requests and improve performance.
*   **Adaptive Rate Limiting:** Manages request frequency to TikTok's servers to prevent triggering rate limits and enhance bot longevity.
*   **Dynamic User-Agent Rotation:** Cycles through a predefined list of user agents to mimic different browsers, making requests less identifiable as bot traffic.
*   **Smart URL Handling:** Includes utilities to resolve TikTok video URLs and accurately extract video IDs.
*   **Robust HTML Scraping:** Locates and parses specific JSON script tags within TikTok page HTML to extract structured data reliably.
*   **Modular Design:** Clearly separated functions for fetching data, managing cache, and handling API requests, allowing for easy expansion.
*   **Development Tools:** Includes `nodemon` for automatic server restarts during development, enhancing developer workflow.

## Tech Stack

*   **Primary Language:** JavaScript
*   **Runtime Environment:** Node.js
*   **Web Framework:** Express.js
*   **HTTP Client:** Axios
*   **Development Tooling:** Nodemon
*   **Data Structures:** JavaScript `Map` for caching

## Installation

To get this project up and running on your local machine, follow these steps:

### Prerequisites

*   Node.js (LTS version recommended)
*   npm (comes with Node.js)

### Steps

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/hsvob972-eng/3rd_perfect_bot.git
    cd 3rd_perfect_bot
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

## Environment Variables

The application currently hardcodes several configuration values within `index.js`. For production deployments and better configurability, it's highly recommended to externalize these into environment variables.

You can create a `.env` file in the root directory of the project and define these variables:

```
PORT=3000
CACHE_DURATION_MS=300000  # 5 minutes in milliseconds
MIN_REQUEST_INTERVAL_MS=5000 # 5 seconds in milliseconds
```

*   `PORT`: The port on which the Express server will listen.
    *   *Default (if not set):* `3000`
*   `CACHE_DURATION_MS`: The duration (in milliseconds) for which TikTok video statistics are cached.
    *   *Default (if not set):* `300000` (5 minutes)
*   `MIN_REQUEST_INTERVAL_MS`: The minimum time (in milliseconds) to wait between requests for the same TikTok video to avoid rate limiting.
    *   *Default (if not set):* `5000` (5 seconds)

**Note:** You would need to integrate a library like `dotenv` to load these variables into `process.env` in `index.js`.

## Usage

### Starting the Server

To start the server, use one of the following commands:

*   **Production Mode:**
    ```bash
    npm start
    ```
    This will start the server using `node index.js`.

*   **Development Mode:**
    ```bash
    npm run dev
    ```
    This will start the server using `nodemon`, which automatically restarts the server when file changes are detected.

Once the server is running, it will be accessible at `http://localhost:<PORT>`.

### API Endpoints

The bot exposes an API endpoint to fetch TikTok video statistics.

#### `GET /api/tiktok/stats`

Fetches detailed statistics for a given TikTok video URL.

*   **Method:** `GET`
*   **Query Parameters:**
    *   `url`: **(Required)** The full URL of the TikTok video.

*   **Example Request:**
    ```bash
    curl -X GET "http://localhost:3000/api/tiktok/stats?url=https://www.tiktok.com/@tiktok/video/7309972322309832962"
    ```

*   **Example Response (Success):**
    ```json
    {
      "success": true,
      "data": {
        "videoId": "7309972322309832962",
        "url": "https://www.tiktok.com/@tiktok/video/7309972322309832962",
        "title": "Your feed is about to get a whole lot more fun. Welcome to TikTok!",
        "author": "@tiktok",
        "stats": {
          "viewCount": "12345678",
          "likeCount": "123456",
          "commentCount": "1234",
          "shareCount": "123"
        },
        "cached": false,
        "timestamp": "2023-11-20T12:00:00.000Z"
      }
    }
    ```

*   **Example Response (Error):**
    ```json
    {
      "success": false,
      "message": "Invalid TikTok URL provided or video not found."
    }
    ```

### Bot Status Monitoring (Future Expansion)

The `botStatus` object in `index.js` is intended as a placeholder for operational state and performance metrics. In future iterations, this could be extended to expose endpoints for:

*   Checking if the bot is running.
*   Monitoring success/failure rates of view increments.
*   Setting target views for specific videos.
*   Managing bot operations (start, stop, pause).

## Contributing

Contributions are welcome! If you have suggestions for improvements, new features, or bug fixes, please follow these steps:

1.  **Fork** the repository.
2.  **Create a new branch** for your feature or bug fix:
    ```bash
    git checkout -b feature/your-feature-name
    ```
    or
    ```bash
    git checkout -b bugfix/issue-description
    ```
3.  **Make your changes** and commit them with a descriptive message.
4.  **Push your branch** to your forked repository.
5.  **Open a Pull Request** to the `main` branch of the original repository, describing your changes and their benefits.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```
