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

### Quick Start with Docker

1. Clone the repository
2. Run the entire stack:
   ```bash
   docker-compose up --build
   ```
3. Access the application:
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8000
   - Django Admin: http://localhost:8000/admin

### Local Development

#### Setup (One-time)
```bash
# Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install all dependencies
npm run install:all
```

#### Running the Application
```bash
# Start both frontend and backend concurrently
npm run dev

# Or start them separately:
npm run start:backend  # Django server on :8000
npm run start:frontend # React Native Web on :3000
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

## 🤝 Contributing

1. Create feature branches
2. Follow the established code style
3. Write tests for new features
4. Update documentation as needed

## 📄 License

[Add your license here] 