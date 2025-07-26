# Foundation PWA

A Progressive Web Application for a foundation, built with React Native Web and Django.

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        Foundation PWA                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────┐ │
│  │   Frontend      │    │    Backend      │    │  Database   │ │
│  │                 │    │                 │    │             │ │
│  │ React Native    │◄──►│     Django      │◄──►│ PostgreSQL  │ │
│  │      Web        │    │   REST API      │    │             │ │
│  │                 │    │                 │    │             │ │
│  │ • Expo CLI      │    │ • DRF           │    │ • Data      │ │
│  │ • Navigation    │    │ • Authentication│    │ • Migrations│ │
│  │ • Styled Comp   │    │ • CORS          │    │ • Relations │ │
│  │ • React Query   │    │ • JWT           │    │             │ │
│  └─────────────────┘    └─────────────────┘    └─────────────┘ │
│           │                       │                    │        │
│           └───────────────────────┼────────────────────┘        │
│                                   │                             │
│  ┌─────────────────────────────────┼─────────────────────────────┐ │
│  │           Docker Compose        │                             │ │
│  │                                 │                             │ │
│  │ • Container Orchestration       │                             │ │
│  │ • Network Management            │                             │ │
│  │ • Volume Management             │                             │ │
│  │ • Environment Variables         │                             │ │
│  └─────────────────────────────────┴─────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

## 📁 Project Structure

```
Cracks/
├── frontend/                 # React Native Web (Expo)
│   ├── src/
│   │   ├── screens/         # Screen components
│   │   ├── components/      # Reusable components
│   │   ├── services/        # API services
│   │   └── styles/          # Styled components
│   ├── App.js              # Main app component
│   ├── package.json        # Frontend dependencies
│   └── Dockerfile          # Frontend container
│
├── backend/                 # Django REST API
│   ├── foundation/         # Django project settings
│   ├── apps/              # Django applications
│   ├── manage.py          # Django management
│   └── Dockerfile         # Backend container
│
├── venv/                   # Python virtual environment
├── requirements.txt        # Python dependencies
├── package.json           # Root scripts & dev tools
├── docker-compose.yml     # Container orchestration
└── README.md             # This file
```

## 🛠️ Tech Stack

### Frontend
- **React Native Web**: Cross-platform development (web + mobile)
- **Expo CLI**: Development platform and build tools
- **React Navigation**: Navigation between screens
- **Styled Components**: Styling and theming
- **React Query**: Data fetching and caching
- **Axios**: HTTP client for API calls

### Backend
- **Django 4.2.7**: Web framework
- **Django REST Framework**: API development
- **PostgreSQL**: Database
- **Django CORS Headers**: Cross-origin resource sharing
- **Django Allauth**: Authentication
- **JWT**: Token-based authentication

### DevOps
- **Docker**: Containerization
- **Docker Compose**: Multi-container orchestration
- **Nginx**: Reverse proxy (production)

## 🚀 Features (Planned)

1. **Phase 1**: Informative homepage with navigation
2. **Phase 2**: Client subscription forms
3. **Phase 3**: Donation payment system
4. **Phase 4**: Shopping cart and donation gifts

## 🏃‍♂️ Getting Started

### Prerequisites
- Docker and Docker Compose
- Node.js 18+ (for local development)
- Python 3.11+ (for local development)

### Quick Commands Reference
```bash
# Start everything with Docker (Universal Mode)
docker-compose up --build

# Frontend development
docker exec cracks-pwa-frontend-1 npm start

# Frontend web-only
docker exec cracks-pwa-frontend-1 npm run web

# Backend shell
docker exec cracks-pwa-backend-1 python manage.py shell

# View logs
docker-compose logs -f

# Stop everything
docker-compose down
```

### Quick Start with Docker

1. Clone the repository
2. Run the entire stack:
   ```bash
   docker-compose up --build
   ```
3. Access the application:
   - Frontend: http://localhost:3002
   - Backend API: http://localhost:8000
   - Django Admin: http://localhost:8000/admin

### Port Mapping Summary

| Service | Port | Description |
|---------|------|-------------|
| Backend API | 8000 | Django REST API |
| Frontend (Web) | 3000 | Web application |
| Expo DevTools | 19000 | Mobile debugging tools |

### Local Development

#### Setup (One-time)
```bash
# Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install Python dependencies
pip install -r requirements.txt

# Install Node.js dependencies
cd frontend
npm install --legacy-peer-deps

# Return to root
cd ..
```

#### Running the Application

**Option 1: Start both frontend and backend concurrently**
```bash
# Make sure virtual environment is activated
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Start both servers
npm run dev
```

**Option 2: Start them separately**

**Terminal 1 - Backend:**
```bash
# Activate virtual environment
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Start Django server
cd backend
python manage.py runserver
# Backend will be available at: http://localhost:8000
```

**Terminal 2 - Frontend:**
```bash
# Start React Native Web development server
cd frontend
npm start
# Frontend will be available at: http://localhost:3000
```

#### Development Commands

**Frontend Development:**
```bash
cd frontend

# Start development server
npm start

# Build for web
npm run web

# Clear cache and restart
npm start -- --clear

# Install new dependencies
npm install --legacy-peer-deps
```

**Backend Development:**
```bash
# Activate virtual environment first
source venv/bin/activate  # On Windows: venv\Scripts\activate

cd backend

# Run Django server
python manage.py runserver

# Create migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Create superuser
python manage.py createsuperuser

# Django shell
python manage.py shell
```

## 🔧 Development Workflow

### Frontend Development
- **Hot Reloading**: Expo provides instant updates
- **Cross-platform**: Test on web, iOS, and Android
- **Component Library**: Reusable styled components
- **State Management**: React Query for server state

### Backend Development
- **Auto-reload**: Django development server
- **API Testing**: Django REST Framework browsable API
- **Database**: PostgreSQL with migrations
- **Authentication**: JWT tokens

### Docker Development
- **Isolated Environment**: Consistent across team
- **Service Discovery**: Automatic networking
- **Volume Mounting**: Live code updates
- **Environment Variables**: Centralized configuration

#### Development Mode

**Universal Mode (Recommended):**
```bash
docker-compose up --build
```
- Frontend runs in universal mode (`npm start`)
- Supports web, iOS, and Android development
- Includes Expo DevTools for mobile debugging
- Access at: http://localhost:3000 (Web)
- Access at: http://localhost:19000 (Expo DevTools)

#### Docker Development Commands

**Frontend Commands:**
```bash
# Universal Development (Web + Mobile)
docker exec cracks-pwa-frontend-1 npm start

# Web-only Development
docker exec cracks-pwa-frontend-1 npm run web

# Check available scripts
docker exec cracks-pwa-frontend-1 npm run
```

**Backend Commands:**
```bash
# Django shell
docker exec cracks-pwa-backend-1 python manage.py shell

# Create superuser
docker exec cracks-pwa-backend-1 python manage.py createsuperuser

# Check migrations
docker exec cracks-pwa-backend-1 python manage.py showmigrations

# Run tests
docker exec cracks-pwa-backend-1 python manage.py test
```

**General Docker Commands:**
```bash
# View logs
docker-compose logs -f frontend
docker-compose logs -f backend

# Restart specific service
docker-compose restart frontend
docker-compose restart backend

# Access container shell
docker exec -it cracks-pwa-frontend-1 sh
docker exec -it cracks-pwa-backend-1 sh

# Stop all services
docker-compose down

# Rebuild and start
docker-compose up --build
```

## 📦 Container Architecture

### Services Overview
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │    Backend      │    │   Database      │
│   (Port 3000)   │    │   (Port 8000)   │    │   (Port 5432)   │
│                 │    │                 │    │                 │
│ • React Native  │    │ • Django        │    │ • PostgreSQL    │
│ • Expo Web      │    │ • REST API      │    │ • Data Storage  │
│ • Navigation    │    │ • Admin Panel   │    │ • Migrations    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
                    ┌─────────────────┐
                    │  Docker Network │
                    │ foundation_net  │
                    └─────────────────┘
```

### Volume Management
- **postgres_data**: Persistent database storage
- **static_volume**: Django static files
- **media_volume**: User uploaded files
- **node_modules**: Frontend dependencies

## 🔐 Environment Variables

### Frontend (.env)
```
REACT_APP_API_URL=http://localhost:8000/api
REACT_APP_ENVIRONMENT=development
```

### Backend (.env)
```
DEBUG=True
SECRET_KEY=your-secret-key
DATABASE_URL=postgresql://user:password@localhost:5432/foundation_db
ALLOWED_HOSTS=localhost,127.0.0.1
CORS_ALLOWED_ORIGINS=http://localhost:3000,http://127.0.0.1:3000
```

## 📋 Available Scripts

### Root Level (package.json)
```bash
npm run install:backend    # Install Python dependencies
npm run install:frontend   # Install Node.js dependencies
npm run install:all        # Install all dependencies
npm run start:backend      # Start Django server
npm run start:frontend     # Start Expo development server
npm run dev                # Start both servers concurrently
npm run docker:up          # Start all containers
npm run docker:down        # Stop all containers
npm run docker:logs        # View container logs
```

### Frontend (Expo)
```bash
npm start                  # Start Expo development server
npm run web                # Start web version
npm run ios                # Start iOS simulator
npm run android            # Start Android emulator
npm run build              # Build for production
```

## 🧪 Testing

### Backend Testing
```bash
cd backend
python manage.py test
```

### Frontend Testing
```bash
cd frontend
npm test
```

## 🚀 Deployment

### Production Build
```bash
# Build frontend
cd frontend && npm run build

# Build backend
cd backend && python manage.py collectstatic

# Deploy with Docker
docker-compose -f docker-compose.prod.yml up --build
```

## 🔧 Troubleshooting

### Common Issues

**Frontend Issues:**
```bash
# Clear npm cache
npm cache clean --force

# Remove node_modules and reinstall
rm -rf node_modules package-lock.json
npm install --legacy-peer-deps

# Expo issues
npx expo install --fix
```

**Backend Issues:**
```bash
# Database connection issues
python manage.py dbshell

# Migration issues
python manage.py makemigrations
python manage.py migrate

# Static files
python manage.py collectstatic
```

**Virtual Environment Issues:**
```bash
# Recreate virtual environment
rm -rf venv
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Debug Mode

**Frontend Debug:**
```bash
cd frontend
npm start -- --clear
# Open browser dev tools for console errors
```

**Backend Debug:**
```bash
# Activate venv first
source venv/bin/activate
cd backend
python manage.py runserver --verbosity=2
```

## 🤝 Contributing

1. Create feature branches
2. Follow the established code style
3. Write tests for new features
4. Update documentation as needed

## 📄 License

[Add your license here] 