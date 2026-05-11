# 🚛 Sarthix — Logistics Bidding Platform

A B2B freight marketplace connecting **shippers** and **drivers** through competitive bidding, live GPS tracking, and permit compliance — built for the Indian freight market.

---

## 🛠 Tech Stack

| Layer | Tools |
|---|---|
| Frontend | React 18, Vite, TanStack Query, Clerk, Leaflet |
| Backend | Node.js, Express, Clerk JWT middleware |
| Database | Supabase (PostgreSQL + Realtime + Storage) |

---

## 🔄 Workflow

```
Shipper posts shipment
        ↓
Drivers place bids (price + ETA)
        ↓
Shipper accepts best bid → driver assigned
        ↓
Shipper notifies: "Material Loaded"
        ↓
Driver starts transit → GPS tracking begins (every 10s)
        ↓
Driver uploads proof of delivery → marked Delivered
        ↓
Shipper rates driver ⭐
```

---

## 👥 Roles

**Shipper (Company)**
- Post shipments with route, weight, load type, base price
- View & accept bids
- Track driver live on map

**Driver**
- Browse & bid on open shipments
- Manage vehicles and permits
- Upload delivery proof

---

## 🚀 Quick Start

```bash
# Clone
git clone https://github.com/your-username/sarthix.git

# Install
cd frontend && npm install
cd ../backend && npm install

# Run
cd backend && npm run dev    # port 5000
cd frontend && npm run dev   # port 5173
```

### Environment Variables

**Frontend `.env`**
```env
VITE_CLERK_PUBLISHABLE_KEY=pk_test_...
VITE_API_BASE_URL=http://localhost:5000/api
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=eyJ...
```

**Backend `.env`**
```env
PORT=5000
CLERK_SECRET_KEY=sk_test_...
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_SERVICE_ROLE_KEY=eyJ...
```

---

## 🗄 Database (Supabase)

Run migrations in order:
```
supabase/migrations/001_core_schema.sql
supabase/migrations/002_shipment_images.sql
supabase/migrations/003_tracking.sql
```

Create two public storage buckets: `shipment-images` and `vehicle-documents`.

---

## 📡 Key API Routes

| Method | Route | Description |
|---|---|---|
| POST | `/api/users/sync` | Sync user on login |
| GET | `/api/shipments` | All open shipments |
| POST | `/api/bids` | Place a bid |
| POST | `/api/bids/accept` | Accept a bid |
| PATCH | `/api/shipments/:id/location` | Push GPS coordinates |
| PATCH | `/api/shipments/:id/status` | Update shipment status |

All routes require `Authorization: Bearer <clerk_jwt>`.

---

## 📍 Shipment Status Flow

```
open → assigned → in_transit → delivered
                ↘ cancelled
```

---

MIT © 2026 Sarthix Team
