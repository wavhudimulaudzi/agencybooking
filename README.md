# Angency Booking 
This is an agency booking rest service built using java and springboot.

## How to start the app.
You can start the app by building it on docker and exposing port 8080. See instructions below.

1. Clone the repo and cd into agencybooking make sure that in your directory you can access Dockerfile
2. Execute the command
   ```sh
   docker build -t my-agency-app .
   ```
3. After creating the container you can run it using this command
    ```sh
   docker run -p 8080:8080 -d my-agency-app 
   ```
4. If everything went well this should run on http://localhost:8080, alternatively you can just run on your IDE (Using IDE's like intellij makes it easy to run spring boot apps)


## Booking Agency API

This REST API provides endpoints for managing bookings, guests, and hotels within a booking agency system.

**Prerequisites**

* A running instance of the Spring Boot application exposing the API (typically on http://localhost:8080)

**Base URLs**

All Bookings API endpoints are located under the base URL: `http://localhost:8080/api/bookings` <br />
All Guests API endpoints are located under the base URL: `http://localhost:8080/api/guests` <br />
All Hotels API endpoints are located under the base URL: `http://localhost:8080/api/hotels`

### **Guests** & **Hotels**
The more important api's in Guest and Hotel are the add Guest and Hotel as these need to be inserted before we can add a booking ( booking doesn't exist without a guest or a hotel). Because of time constraints did ran out of time to add more functional api and error handling to these two. <br />

* **Add a Guest** 
  `POST /api/guests` 
  * **Request Body:** JSON object representing the booking (see example below). 
  * **Returns:** The created booking object.
 
**Guest Request Example:**
```json
{
    "name": "wavhudi",
    "surname": "Mulaudzi",
    "email": "mulaudzi@gmail.com",
    "mobileNumber": "072456789",
    "address": "20c corsair rd, cape town, 7441",
    "userOfEntry": "Wavhudi"
}
```
<br />
 
* **Add a Hotel** 
  `POST /api/hotels` 
  * **Request Body:** JSON object representing the booking (see example below). 
  * **Returns:** The created booking object.
 
**Hotel Request Example:**
```json
{
    "name": "HotelSky",
    "email": "hotel@sky.com",
    "telNumber": "9832839",
    "mobileNumber": "728738273",
    "faxNumber":"39283",
    "address": "test",
    "rating": 8,
    "userOfEntry": "Wavhudi"
}
```

### **Bookings**

* **Get all bookings** <br />
The results is pagenated to solve performance issues of trying to return all bookings info. <br />
  `GET /api/bookings`
  Returns a list of booking objects with a default page of 0 and size 3. <br />
  `GET /api/bookings?page=1&size=4` If interested in certain page and size you can just pass int page and size as params.

* **Get a booking by ID**
  `GET /api/bookings/{bookingId}`
  Retrieves a specific booking based on its ID.

* **Add a booking** 
  `POST /api/bookings` 
  * **Request Body:** JSON object representing the booking (see example below). 
  * **Returns:** The created booking object.

* **Update a booking**
  `PUT /api/bookings/{bookingId}`
  * **Request Body:** JSON object with the updated booking fields. See example below <br />
    ```json
      {
          "roomType": "Queen",
          "userOfEntryAndUpdate": "Hope"
      }
    ```
  * **Returns:** The updated booking object.

* **Delete a booking**
  `DELETE /api/bookings/{bookingId}`
  Deletes a booking based on its ID.

**Booking Request Example:**
```json
{
  "guestEmail": "mulaudzi@gmail.com",
  "hotelEmail": "hotel@sky.com",
  "roomType": "King",
  "rooms": 1,
  "adults": 2,
  "children": 0,
  "arrival": "2023-12-20T14:00:00",
  "departure": "2023-12-25T11:00:00",
  "userOfEntryAndUpdate": "wavhudi"
}
```
<br />

`guestEmail` used to identify the guest from the guest table. <br />
`hotelEmail` used to identify the hotel the guest will be staying at in the hotel table. <br />
`userOfEntryAndUpdate` This is just for auditing to keep track of who inserted or updated the record. <br />

## Future Improvements
There are many areas we can improve on here.
* Like from adding more sufficient test coverage
* adding more apis
* formating the json response better using Data transfer objects
* handling cases of duplicated users or booking not found better
* adding some liquidation scripts to control how tables and columns are being created as with hibernate auto generation it just put columns where ever it wants which is not good for database visibility and readability.
