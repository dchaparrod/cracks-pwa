# 🚀 Quick Setup Guide

## Prerequisites

- **Docker & Docker Compose** (recommended)
- **Node.js 18+** (for local development)
- **Python 3.11+** (for local development)
- **Git**

## Option 1: Docker Setup (Recommended)

### 1. Clone and Setup
```bash
git clone <your-repo-url>
cd Cracks
```

### 2. Start All Services
```bash
docker-compose up --build
```

### 3. Access Applications
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8000
- **Django Admin**: http://localhost:8000/admin

## Option 2: Local Development Setup

### 1. Backend Setup
```bash
# Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Setup Django
cd backend
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

### 2. Frontend Setup
```bash
# Install dependencies
cd frontend
npm install --legacy-peer-deps

# Start development server
npm start
```

### 3. Database Setup (Optional)
```bash
# Install PostgreSQL locally or use Docker
docker run --name foundation-db \
  -e POSTGRES_DB=foundation_db \
  -e POSTGRES_USER=foundation_user \
  -e POSTGRES_PASSWORD=foundation_password \
  -p 5432:5432 \
  -d postgres:15-alpine
```

## Development Workflow

### Using Root Scripts
```bash
# Install all dependencies
npm run install:all

# Start both frontend and backend
npm run dev

# Start only backend
npm run start:backend

# Start only frontend
npm run start:frontend
```

### Using Docker
```bash
# Start all services
npm run docker:up

# View logs
npm run docker:logs

# Stop all services
npm run docker:down
```

## Environment Variables

### Create `.env` files:

**Backend (.env)**
```env
DEBUG=True
SECRET_KEY=your-secret-key-here
DATABASE_URL=postgresql://foundation_user:foundation_password@localhost:5432/foundation_db
ALLOWED_HOSTS=localhost,127.0.0.1
CORS_ALLOWED_ORIGINS=http://localhost:3000,http://127.0.0.1:3000
```

**Frontend (.env)**
```env
REACT_APP_API_URL=http://localhost:8000/api
REACT_APP_ENVIRONMENT=development
```

## Common Issues & Solutions

### Frontend Issues
```bash
# Clear npm cache
npm cache clean --force

# Remove node_modules and reinstall
rm -rf node_modules package-lock.json
npm install --legacy-peer-deps

# Expo issues
npx expo install --fix
```

### Backend Issues
```bash
# Database connection issues
python manage.py dbshell

# Migration issues
python manage.py makemigrations
python manage.py migrate

# Static files
python manage.py collectstatic
```

### Docker Issues
```bash
# Clean up containers
docker-compose down -v
docker system prune -a

# Rebuild without cache
docker-compose build --no-cache
```

## Next Steps

1. **Frontend Development**: Start building screens in `frontend/src/screens/`
2. **Backend Development**: Create Django apps in `backend/apps/`
3. **API Integration**: Connect frontend to backend APIs
4. **Styling**: Use styled-components for consistent design
5. **Testing**: Add tests for both frontend and backend

## Useful Commands

```bash
# Django management
python manage.py shell
python manage.py test
python manage.py collectstatic

# Frontend development
npm run web
npm run ios
npm run android

# Docker management
docker-compose ps
docker-compose logs -f backend
docker-compose exec backend python manage.py shell
``` 