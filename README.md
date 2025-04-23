// App.jsx - MIGSAFE Frontend Entry Point
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Home from './pages/Home';
import Checklist from './pages/Checklist';
import ReportScam from './pages/ReportScam';
import Header from './components/Header';
import Footer from './components/Footer';

function App() {
  return (
    <Router>
      <div className="min-h-screen flex flex-col">
        <Header />
        <main className="flex-grow p-4">
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/checklist" element={<Checklist />} />
            <Route path="/report" element={<ReportScam />} />
          </Routes>
        </main>
        <Footer />
      </div>
    </Router>
  );
}

export default App;

// src/pages/Home.jsx
export function Home() {
  return (
    <div className="text-center">
      <h1 className="text-3xl font-bold mb-4">Welcome to MIGSAFE</h1>
      <p>Your trusted companion for safe migration and job search support.</p>
    </div>
  );
}

// src/pages/Checklist.jsx
import React, { useState } from 'react';
import axios from 'axios';

export function Checklist() {
  const [origin, setOrigin] = useState('');
  const [destination, setDestination] = useState('');
  const [jobType, setJobType] = useState('');
  const [checklist, setChecklist] = useState([]);

  const handleSubmit = async (e) => {
    e.preventDefault();
    const res = await axios.post('https://your-backend-url/api/generate-checklist', {
      origin, destination, jobType
    });
    setChecklist(res.data.checklist);
  };

  return (
    <div>
      <h2 className="text-2xl font-semibold mb-4">Generate Safety Checklist</h2>
      <form onSubmit={handleSubmit} className="space-y-3">
        <input className="border p-2 w-full" placeholder="Country of Origin" value={origin} onChange={(e) => setOrigin(e.target.value)} />
        <input className="border p-2 w-full" placeholder="Destination Country" value={destination} onChange={(e) => setDestination(e.target.value)} />
        <input className="border p-2 w-full" placeholder="Job Type" value={jobType} onChange={(e) => setJobType(e.target.value)} />
        <button className="bg-blue-600 text-white px-4 py-2 rounded" type="submit">Generate</button>
      </form>
      <ul className="mt-6 list-disc pl-5">
        {checklist.map((item, index) => (
          <li key={index}>{item}</li>
        ))}
      </ul>
    </div>
  );
}

// src/pages/ReportScam.jsx
import React, { useState } from 'react';

export function ReportScam() {
  const [message, setMessage] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    alert('Report submitted: ' + message);
  };

  return (
    <div>
      <h2 className="text-2xl font-semibold mb-4">Report a Scam</h2>
      <form onSubmit={handleSubmit} className="space-y-3">
        <textarea className="border p-2 w-full" placeholder="Describe the scam..." value={message} onChange={(e) => setMessage(e.target.value)}></textarea>
        <button className="bg-red-600 text-white px-4 py-2 rounded" type="submit">Submit Report</button>
      </form>
    </div>
  );
}

// src/components/Header.jsx
export function Header() {
  return (
    <header className="bg-gray-800 text-white p-4 flex justify-between">
      <h1 className="text-xl font-bold">MIGSAFE</h1>
      <nav className="space-x-4">
        <a href="/" className="hover:underline">Home</a>
        <a href="/checklist" className="hover:underline">Checklist</a>
        <a href="/report" className="hover:underline">Report</a>
      </nav>
    </header>
  );
}

// src/components/Footer.jsx
export function Footer() {
  return (
    <footer className="bg-gray-100 text-center p-4 mt-6">
      <p>&copy; 2025 MIGSAFE. All rights reserved.</p>
    </footer>
  );
}
