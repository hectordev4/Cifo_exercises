# My RentingCar Application Documentation  
  
## What is this Application?  
  
I built the RentingCar application as a full-stack car rental management system using **Spring Boot** for the backend and **React** frontend through the **Hilla** framework. My application allows users to browse available cars, make bookings, and manage their rental profiles, while providing administrators with tools to manage the car fleet and monitor bookings.  
  
## Technology Stack & Architecture  
  
### Backend  
- **Spring Boot** - Java-based framework I chose for the backend  
- **Hilla** - Integration framework I used to connect Spring Boot with React  
- **AWS DynamoDB** - NoSQL database with single-table design I implemented  
- **AWS Cognito** - Authentication and user management system I integrated  
  
### Frontend  
- **React** with **TypeScript** - User interface framework I developed with  
- **Vaadin Components** - UI component library I utilized  
- **Custom Hooks** - State management and API integration patterns I created  
  
## Data Structure & Design  
  
I implemented a sophisticated **dual single-table DynamoDB design** that efficiently organizes data into two main tables:  
  
### Table 1: Delegations (Inventory & Availability) [1](#6-0)   
  
This table stores:  
- **Delegations**: Rental locations with profile information  
- **Cars**: Vehicle inventory with details like make, model, year, price  
- **Calendar**: Availability data for each car  
  
### Table 2: Users (Profiles & Bookings) [2](#6-1)   
  
This table manages:  
- **User Profiles**: Personal information and preferences  
- **Bookings**: Rental transactions with embedded car and delegation data  
  
## Data Flow Architecture  
  
My application follows this data flow pattern I designed:

React Components → Custom Hooks → Hilla Endpoints → Spring Services → DynamoDB Repositories → AWS DynamoDB

  
### Frontend Data Flow  
1. **React Components** I created trigger user actions  
2. **Custom Hooks** I developed manage state and API calls  
3. **Hilla Framework** provides type-safe communication to my backend  
  
### Backend Data Flow  
1. **Hilla Endpoints** I implemented receive frontend requests  
2. **Repository Layer** I built handles DynamoDB operations  
3. **DynamoDB Configuration** I set up manages AWS connections  
  
## Custom Hooks Implementation  
  
I've implemented custom hooks for state management and API integration:  
  
### ListCars Component with Booking Logic  
My `ListCars` component includes sophisticated booking hash generation I developed: [3](#6-2)   
  
This demonstrates my implementation of:  
- **SHA-256 hash generation** for unique booking identifiers  
- **TypeScript interfaces** for type safety  
- **Async/await patterns** for API calls  
  
## AWS Cognito Authentication Implementation  
  
I've implemented a comprehensive authentication system using AWS Cognito:  
  
### Authentication Workflow  
  
I implemented a comprehensive authentication system using AWS Cognito that serves as the main entry point for managing routing and authentication checks. The workflow I built includes:  
  
- **Application Entry (App.jsx)**: The main component I created that manages routing and authentication checks using `BrowserRouter` and `Routes` from `react-router-dom`. The `isAuthenticated` function I implemented checks for an `accessToken` in `sessionStorage` and handles route protection.  
  
- **Route Management**: My system handles multiple routes including:  
  - `/`: Redirects to `/home` if authenticated, else to `/login`  
  - `/login`: Renders `LoginPage`  
  - `/confirm`: Renders `ConfirmUserPage`   
  - `/home`: Renders `HomePage` if authenticated, else redirects to `/login`  
  - `/forgot`: Renders `ForgotPassword` [4](#6-3)   
  
### Sign-In/Sign-Up Process  
My authentication handles multiple user flows I designed: [5](#6-4)   
  
### Account Management Features  
The system includes complete user lifecycle management I built: [6](#6-5)   
  
### Authentication Service Integration  
My backend integrates with Cognito through dedicated services I created: [7](#6-6)   
  
## Key Features I've Implemented  
  
### ✅ Completed Features  
1. **Car Listing System** - I built a system to browse available vehicles with images and details  
2. **Booking System** - I created hash-based booking generation and management  
3. **AWS Cognito Authentication** - I implemented a complete user authentication workflow  
4. **DynamoDB Integration** - I designed a dual single-table structure for scalability  
5. **TypeScript Integration** - I ensured type-safe frontend development  
6. **User Profile Management** - I built account creation and management features  
  
### 🔄 Features In Progress  
1. **Calendar Interface** - I'm working on date selection for rentals  
2. **Admin Dashboard** - I'm developing fleet management and booking monitoring  
3. **Advanced Booking Management** - I'm building the complete booking lifecycle  
  
## How My Application Works  
  
1. **User Registration/Login**: Users authenticate through AWS Cognito with email verification I configured  
2. **Car Browsing**: Users view available cars fetched from DynamoDB via Hilla endpoints I created  
3. **Booking Process**: Users select cars and generate unique booking hashes through my system  
4. **Data Persistence**: All data is stored in DynamoDB using the optimized single-table design I implemented  
5. **State Management**: React hooks I developed manage frontend state and API communication  
  
## Documentation References  
  
For complete technical details, refer to the documentation I've created:  
- [AWS DynamoDB Guide](docs/1-AWS-dynamoDB.md)  
- [Spring Boot Vaadin Integration](docs/2-SpringBoot-Vaadin.md)  
- [Authentication Workflow](docs/core-concepts/auth/cognito-AWS-react/Authentication%20Workflow.md)  
- [Project Requirements](docs/PRA/PRA#06-FullStack_%20Renting%20Car_V1.1.md)  
  
My implementation demonstrates my understanding of modern full-stack development patterns, cloud-native architecture, and scalable data design principles.  
