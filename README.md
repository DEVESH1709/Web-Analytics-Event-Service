# Web Analytics Event Service

A backend and frontend system to collect, store, and analyze user interaction events (view, click, location) using Node.js, Express.js, and MongoDB.

##  Setup Instructions (Windows)

### 1. Install Requirements

- [Node.js](https://nodejs.org/) (v18+ recommended)
- [MongoDB](https://www.mongodb.com/try/download/community) (local instance)

Verify installation:
```bash
node -v
npm -v
mongod --version
```

Start MongoDB service if it's not running:
```bash
mongod 
```

2. Clone Repository:
```bash
git clone https://github.com/DEVESH1709/Web-Analytics-Event-Service.g
cd <repo-folder>
```

4. Backend Setup:
 ```bash
cd backend
npm install 
```

Create a .env file:
```bash  
MONGO_URI
PORT
```

4. Generate Sample Data:
```bash
node scripts/generateData.js
```

6. Start Backend Server:
```bash   
npm start
```

8. Frontend Setup:
```bash
cd ../frontend
npx http-server .
```

--> API Endpoints
| Description  | Create a new event |
| ------------ | ------------------ |
| Method       | POST               |
| Content-Type | application/json   |

Body Example (for click):
```bash
{
  "user_id": "user123",
  "event_type": "click",
  "timestamp": "2025-05-20T12:00:00Z",
  "payload": {
    "element_id": "btn-login",
    "text": "Login",
    "xpath": "/html/body/button"
  }
}
```

Success: 201 Created
Errors: 400 Bad Request, 500 Internal Server Error

GET /analytics/event-counts
| Description | Get total event count (with filters) |
| ----------- | ------------------------------------ |
| Method      | GET                                  |

Query Parameters (optional):

1-event_type=view

2-start_date=2025-05-01

3-end_date=2025-05-29

GET /analytics/event-counts-by-type
| Description | Get count grouped by event\_type |
| ----------- | -------------------------------- |
| Method      | GET                              |

Query Parameters (optional):

1-start_date=2025-05-01
2-end_date=2025-05-29

```bash
 GET /analytics/event-counts-by-type?start_date=2025-05-01&end_date=2025-05-29
```

```bash
[
  { "event_type": "view", "count": 2100 },
  { "event_type": "click", "count": 1200 },
  { "event_type": "location", "count": 800 }
]
```

--> Technologies Used
 
| Tech          | Purpose                        |
| ------------- | ------------------------------ |
| Node.js       | Server-side JavaScript runtime |
| Express.js    | Web framework for routing/API  |
| MongoDB       | NoSQL database                 |
| Mongoose      | ODM for MongoDB schema/queries |
| Faker.js      | Data generation for testing    |
| HTML/JS       | Frontend UI and event triggers |
| ServiceWorker | Async background event posting |
| Morgan        | Logging HTTP requests          |

--> Database Schema (events) :
```bash
{
  user_id: String,
  event_type: "view" | "click" | "location",
  timestamp: Date,
  payload: Object
}
```
1- Indexed fields: event_type, timestamp

2- payload varies based on event type

3- timestamp used for date filtering

--> Testing with Postman

1- POST /events: Send valid JSON events

2- GET /analytics/event-counts: Try with and without filters

3- GET /analytics/event-counts-by-type: View grouped results


-->  Challenges Faced

1- Handling flexible payload validation

2- Ensuring accurate UTC timestamps

3- MongoDB aggregation with dynamic filters

4- IP whitelisting for Atlas (initially)

-->  Future Improvements

1- Auth/API keys for secure tracking

2- Analytics dashboard with charts

3- Caching frequent queries (Redis)

4- Batch event API support

5- Geolocation clustering with geospatial indexing

6-Cloud deployment with Docker + CI/CD

7- Service Worker scope and async fetch handling
