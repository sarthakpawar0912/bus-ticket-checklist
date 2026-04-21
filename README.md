{
  "info": {
    "_postman_id": "bus-ticket-booking-system-api",
    "name": "Bus Ticket Booking System API",
    "description": "# 🚌 Bus Ticket Booking System API Collection\n\n## How to Use This Collection\n\n1. **Import this file into Postman:**\n   - Open Postman → File → Import → drag this `.json` file\n   - Collection appears in the left sidebar\n\n2. **Set variables** (Collection → Variables tab):\n   - `baseUrl` — default `http://localhost:8080`\n   - `adminUser` — default `admin`\n   - `adminPassword` — set to your backend's `APP_ADMIN_PASSWORD`\n\n3. **Start the backend:**\n   ```powershell\n   cd \"C:\\Users\\Sarthak\\OneDrive\\Desktop\\gs studeis\\bus-ticket-booking-system\"\n   $env:APP_ADMIN_PASSWORD = \"admin1234\"\n   .\\mvnw.cmd spring-boot:run\n   ```\n\n4. **Click any request → Send.** HTTP Basic auth is pre-configured at collection level.\n\n## Covered Endpoints\n\n- Trip (list, search, get by ID)\n- Booking (create, get, download ticket)\n- Payment (process, get, download ticket, group ticket)\n- Customer (list, create, get by ID)\n- Review (list, create)\n- Agency, Bus, Driver, Route (basic CRUD)\n\n## Tips for Viva\n\n- Use the **\"1 - Health Check\"** folder first — proves backend is up.\n- Demo **\"3 - Booking Flow\"** end-to-end — shows real data moving through the system.\n- Open the **\"Console\" tab** (bottom-left) during viva — shows the actual HTTP request/response including the `Authorization: Basic` header.",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "auth": {
    "type": "basic",
    "basic": [
      { "key": "username", "value": "{{adminUser}}", "type": "string" },
      { "key": "password", "value": "{{adminPassword}}", "type": "string" }
    ]
  },
  "variable": [
    { "key": "baseUrl", "value": "http://localhost:8080", "type": "string" },
    { "key": "adminUser", "value": "admin", "type": "string" },
    { "key": "adminPassword", "value": "admin1234", "type": "string" }
  ],
  "item": [
    {
      "name": "1 - Health & Auth Check",
      "item": [
        {
          "name": "Unauthed call (should 401)",
          "request": {
            "auth": { "type": "noauth" },
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/trips", "host": ["{{baseUrl}}"], "path": ["api", "trips"] },
            "description": "Proves the security chain is working — returns 401 without credentials."
          }
        },
        {
          "name": "Authed call (should 200)",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/trips", "host": ["{{baseUrl}}"], "path": ["api", "trips"] },
            "description": "Inherits Basic auth from collection — returns the full trip list."
          }
        }
      ]
    },
    {
      "name": "2 - Trips",
      "item": [
        {
          "name": "Get all trips",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/trips", "host": ["{{baseUrl}}"], "path": ["api", "trips"] }
          }
        },
        {
          "name": "Get trip by ID",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/trips/1", "host": ["{{baseUrl}}"], "path": ["api", "trips", "1"] }
          }
        },
        {
          "name": "Search trips (from, to)",
          "request": {
            "method": "GET",
            "url": {
              "raw": "{{baseUrl}}/api/trips/search?from=Mumbai&to=Pune",
              "host": ["{{baseUrl}}"],
              "path": ["api", "trips", "search"],
              "query": [
                { "key": "from", "value": "Mumbai" },
                { "key": "to", "value": "Pune" }
              ]
            }
          }
        },
        {
          "name": "Get trips paginated",
          "request": {
            "method": "GET",
            "url": {
              "raw": "{{baseUrl}}/api/trips/page?page=0&size=10",
              "host": ["{{baseUrl}}"],
              "path": ["api", "trips", "page"],
              "query": [
                { "key": "page", "value": "0" },
                { "key": "size", "value": "10" }
              ]
            }
          }
        }
      ]
    },
    {
      "name": "3 - Booking Flow",
      "item": [
        {
          "name": "Initiate booking (2 seats)",
          "request": {
            "method": "POST",
            "header": [{ "key": "Content-Type", "value": "application/json" }],
            "body": {
              "mode": "raw",
              "raw": "{\n  \"tripId\": 1,\n  \"seatNumbers\": [3, 4],\n  \"customerId\": 1\n}"
            },
            "url": { "raw": "{{baseUrl}}/api/bookings", "host": ["{{baseUrl}}"], "path": ["api", "bookings"] },
            "description": "Books 2 seats. Service uses pessimistic row lock (SELECT FOR UPDATE) to prevent double-booking."
          }
        },
        {
          "name": "Get bookings for trip",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/bookings/trip/1", "host": ["{{baseUrl}}"], "path": ["api", "bookings", "trip", "1"] }
          }
        },
        {
          "name": "Get booking by ID",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/bookings/1", "host": ["{{baseUrl}}"], "path": ["api", "bookings", "1"] }
          }
        },
        {
          "name": "Download single-seat ticket PDF",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/bookings/1/ticket", "host": ["{{baseUrl}}"], "path": ["api", "bookings", "1", "ticket"] },
            "description": "Returns a PDF. In Postman: click Send → Save Response → Save to a file → open in PDF viewer."
          }
        },
        {
          "name": "Download group ticket PDF",
          "request": {
            "method": "GET",
            "url": {
              "raw": "{{baseUrl}}/api/bookings/group-ticket?bookingIds=1,2,3",
              "host": ["{{baseUrl}}"],
              "path": ["api", "bookings", "group-ticket"],
              "query": [{ "key": "bookingIds", "value": "1,2,3" }]
            }
          }
        }
      ]
    },
    {
      "name": "4 - Payment Flow",
      "item": [
        {
          "name": "Process payment",
          "request": {
            "method": "POST",
            "header": [{ "key": "Content-Type", "value": "application/json" }],
            "body": {
              "mode": "raw",
              "raw": "{\n  \"bookingId\": 1,\n  \"customerId\": 1,\n  \"amount\": 500.00\n}"
            },
            "url": { "raw": "{{baseUrl}}/api/payments", "host": ["{{baseUrl}}"], "path": ["api", "payments"] }
          }
        },
        {
          "name": "Get all payments",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/payments", "host": ["{{baseUrl}}"], "path": ["api", "payments"] }
          }
        },
        {
          "name": "Get payment by ID",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/payments/1", "host": ["{{baseUrl}}"], "path": ["api", "payments", "1"] }
          }
        },
        {
          "name": "Get payment by booking ID",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/payments/booking/1", "host": ["{{baseUrl}}"], "path": ["api", "payments", "booking", "1"] }
          }
        },
        {
          "name": "Get payments by customer",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/payments/customer/1", "host": ["{{baseUrl}}"], "path": ["api", "payments", "customer", "1"] }
          }
        },
        {
          "name": "Download payment ticket PDF",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/payments/1/ticket", "host": ["{{baseUrl}}"], "path": ["api", "payments", "1", "ticket"] }
          }
        },
        {
          "name": "Download group-payment ticket PDF",
          "request": {
            "method": "GET",
            "url": {
              "raw": "{{baseUrl}}/api/payments/group-ticket?paymentIds=1,2,3",
              "host": ["{{baseUrl}}"],
              "path": ["api", "payments", "group-ticket"],
              "query": [{ "key": "paymentIds", "value": "1,2,3" }]
            },
            "description": "Round 4 fix: CSV parse errors now return 400 Bad Request instead of 500."
          }
        },
        {
          "name": "Download group-payment (bad CSV — expect 400)",
          "request": {
            "method": "GET",
            "url": {
              "raw": "{{baseUrl}}/api/payments/group-ticket?paymentIds=abc",
              "host": ["{{baseUrl}}"],
              "path": ["api", "payments", "group-ticket"],
              "query": [{ "key": "paymentIds", "value": "abc" }]
            },
            "description": "Verifies the Round 4 fix — bad CSV input now returns clean 400, not 500."
          }
        }
      ]
    },
    {
      "name": "5 - Customers",
      "item": [
        {
          "name": "Get all customers",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/customers", "host": ["{{baseUrl}}"], "path": ["api", "customers"] }
          }
        },
        {
          "name": "Get customer by ID",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/customers/1", "host": ["{{baseUrl}}"], "path": ["api", "customers", "1"] }
          }
        },
        {
          "name": "Create customer",
          "request": {
            "method": "POST",
            "header": [{ "key": "Content-Type", "value": "application/json" }],
            "body": {
              "mode": "raw",
              "raw": "{\n  \"name\": \"Demo Customer\",\n  \"email\": \"demo@example.com\",\n  \"phone\": \"9876543210\",\n  \"addressId\": 1\n}"
            },
            "url": { "raw": "{{baseUrl}}/api/customers", "host": ["{{baseUrl}}"], "path": ["api", "customers"] }
          }
        }
      ]
    },
    {
      "name": "6 - Reviews",
      "item": [
        {
          "name": "Get all reviews",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/reviews", "host": ["{{baseUrl}}"], "path": ["api", "reviews"] }
          }
        },
        {
          "name": "Get reviews for trip",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/reviews/trip/1", "host": ["{{baseUrl}}"], "path": ["api", "reviews", "trip", "1"] }
          }
        },
        {
          "name": "Create review",
          "request": {
            "method": "POST",
            "header": [{ "key": "Content-Type", "value": "application/json" }],
            "body": {
              "mode": "raw",
              "raw": "{\n  \"customerId\": 1,\n  \"tripId\": 1,\n  \"rating\": 5,\n  \"comment\": \"Great service!\"\n}"
            },
            "url": { "raw": "{{baseUrl}}/api/reviews", "host": ["{{baseUrl}}"], "path": ["api", "reviews"] }
          }
        }
      ]
    },
    {
      "name": "7 - Agency / Office / Bus / Driver",
      "item": [
        {
          "name": "Get all agencies",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/agencies", "host": ["{{baseUrl}}"], "path": ["api", "agencies"] }
          }
        },
        {
          "name": "Get all offices",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/agencies/offices", "host": ["{{baseUrl}}"], "path": ["api", "agencies", "offices"] }
          }
        },
        {
          "name": "Get all buses",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/buses", "host": ["{{baseUrl}}"], "path": ["api", "buses"] }
          }
        },
        {
          "name": "Get all drivers",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/drivers", "host": ["{{baseUrl}}"], "path": ["api", "drivers"] }
          }
        },
        {
          "name": "Get all routes",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/routes", "host": ["{{baseUrl}}"], "path": ["api", "routes"] }
          }
        },
        {
          "name": "Get all addresses",
          "request": {
            "method": "GET",
            "url": { "raw": "{{baseUrl}}/api/addresses", "host": ["{{baseUrl}}"], "path": ["api", "addresses"] }
          }
        }
      ]
    }
  ]
}

