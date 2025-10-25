// src/index.js
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);

// src/App.js
import React from "react";
import { Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import SearchResults from "./pages/SearchResults";
import Booking from "./pages/Booking";
import BookingConfirmation from "./components/BookingConfirmation";

function App() {
  return (
    <div>
      <h1 style={{ textAlign: "center" }}>✈️ Flight Booking Simulator</h1>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/search" element={<SearchResults />} />
        <Route path="/booking/:flightId" element={<Booking />} />
        <Route path="/confirmation/:pnr" element={<BookingConfirmation />} />
      </Routes>
    </div>
  );
}
export default App;

// src/pages/Home.js
import React from "react";
import FlightSearch from "../components/FlightSearch";
function Home() {
  return (
    <div>
      <FlightSearch />
    </div>
  );
}
export default Home;

// src/components/FlightSearch.js
import React, { useState } from "react";
import { useNavigate } from "react-router-dom";

function FlightSearch() {
  const [source, setSource] = useState("");
  const [destination, setDestination] = useState("");
  const navigate = useNavigate();
  const handleSearch = () => {
    if (source && destination) {
      navigate(`/search?source=${source}&destination=${destination}`);
    } else {
      alert("Please enter both source and destination");
    }
  };
  return (
    <div style={{ textAlign: "center" }}>
      <h2>Search Flights</h2>
      <input
        type="text"
        placeholder="Source"
        value={source}
        onChange={(e) => setSource(e.target.value)}
      />
      <input
        type="text"
        placeholder="Destination"
        value={destination}
        onChange={(e) => setDestination(e.target.value)}
      />
      <button onClick={handleSearch}>Search</button>
    </div>
  );
}
export default FlightSearch;

// src/pages/SearchResults.js
import React, { useEffect, useState } from "react";
import { useLocation } from "react-router-dom";
import FlightCard from "../components/FlightCard";
import api from "../services/api";

function useQuery() {
  return new URLSearchParams(useLocation().search);
}
function SearchResults() {
  const query = useQuery();
  const source = query.get("source");
  const destination = query.get("destination");
  const [flights, setFlights] = useState([]);

  useEffect(() => {
    async function fetchFlights() {
      try {
        const response = await api.get(`/search?source=${source}&destination=${destination}`);
        setFlights(response.data);
      } catch (error) {
        console.error("Error fetching flights:", error);
      }
    }
    if (source && destination) fetchFlights();
  }, [source, destination]);

  return (
    <div style={{ textAlign: "center" }}>
      <h2>Available Flights</h2>
      {flights.length > 0 ? (
        flights.map((flight) => <FlightCard key={flight.flight_id} flight={flight} />)
      ) : (
        <p>No flights found.</p>
      )}
    </div>
  );
}
export default SearchResults;

// src/components/FlightCard.js
import React from "react";
import { useNavigate } from "react-router-dom";

function FlightCard({ flight }) {
  const navigate = useNavigate();
  return (
    <div style={{
        border: "1px solid #ccc",
        margin: "10px",
        padding: "10px",
        borderRadius: "8px",
      }}>
      <h3>{flight.airline}</h3>
      <p>{flight.source} → {flight.destination}</p>
      <p>Departure: {flight.departure_time}</p>
      <p>Price: ₹{flight.price}</p>
      <button onClick={() => navigate(`/booking/${flight.flight_id}`)}>
        Book Now
      </button>
    </div>
  );
}
export default FlightCard;

// src/pages/Booking.js
import React from "react";
import { useParams } from "react-router-dom";
import BookingForm from "../components/BookingForm";

function Booking() {
  const { flightId } = useParams();
  return (
    <div style={{ textAlign: "center" }}>
      <h2>Book Flight</h2>
      <BookingForm flightId={flightId} />
    </div>
  );
}
export default Booking;

// src/components/BookingForm.js
import React, { useState } from "react";
import { useNavigate } from "react-router-dom";
import api from "../services/api";

function BookingForm({ flightId }) {
  const [passengerName, setPassengerName] = useState("");
  const [email, setEmail] = useState("");
  const [seats, setSeats] = useState(1);
  const navigate = useNavigate();

  const handleBooking = async () => {
    try {
      const response = await api.post("/book", {
        flight_id: flightId,
        passenger_name: passengerName,
        email,
        seats,
      });
      navigate(`/confirmation/${response.data.pnr}`);
    } catch (error) {
      alert("Booking failed!");
      console.error(error);
    }
  };

  return (
    <div>
      <input
        type="text"
        placeholder="Passenger Name"
        value={passengerName}
        onChange={(e) => setPassengerName(e.target.value)}
      />
      <input
        type="email"
        placeholder="Email Address"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <input
        type="number"
        min="1"
        placeholder="Seats"
        value={seats}
        onChange={(e) => setSeats(e.target.value)}
      />
      <button onClick={handleBooking}>Confirm Booking</button>
    </div>
  );
}
export default BookingForm;

// src/components/BookingConfirmation.js
import React, { useEffect, useState } from "react";
import { useParams } from "react-router-dom";
import api from "../services/api";

function BookingConfirmation() {
  const { pnr } = useParams();
  const [details, setDetails] = useState(null);

  useEffect(() => {
    async function fetchDetails() {
      try {
        const response = await api.get(`/booking/${pnr}`);
        setDetails(response.data);
      } catch (error) {
        console.error("Error fetching booking details:", error);
      }
    }
    fetchDetails();
  }, [pnr]);

  return (
    <div style={{ textAlign: "center" }}>
      <h2>Booking Confirmation</h2>
      {details ? (
        <div>
          <p><b>PNR:</b> {details.pnr}</p>
          <p><b>Passenger:</b> {details.passenger_name}</p>
          <p><b>Flight:</b> {details.flight_id}</p>
          <p><b>Seats:</b> {details.seats}</p>
          <p><b>Total Price:</b> ₹{details.total_price}</p>
          <button onClick={() => window.print()}>Download Receipt</button>
        </div>
      ) : (
        <p>Loading...</p>
      )}
    </div>
  );
}
export default BookingConfirmation;

// src/services/api.js
import axios from "axios";
const api = axios.create({
  baseURL: "http://127.0.0.1:8000", // backend FastAPI server
});
export default api;
