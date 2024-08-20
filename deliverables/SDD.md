# MARCO - Software Design Document

## Title Page

### Project Name
**MARCO - Smart Shopping Assistant**

### Vision Statement
**MARCO aims to revolutionize the grocery shopping experience by seamlessly integrating nutrition tracking, inventory management, and price comparison into a single platform. Our vision is to empower users to make healthier, smarter, and more cost-effective food choices while reducing food waste and simplifying meal planning.**


## System Design Document

### System Architecture
### **Updated System Architecture**

The architecture of MARCO leverages modern, scalable, and efficient technologies to provide a seamless user experience. The system is designed with a focus on real-time data management, flexible API interactions, and a responsive user interface.

#### **System Architecture Components:**

1. **Frontend (User Interface):**
   - **Framework:** React.js (for web) and React Native (for mobile)
   - **Styling:** Tailwind CSS for designing a consistent, responsive, and highly customizable user interface.
   - **State Management:** Redux or React Context API for managing global application state.
   - **GraphQL Client:** Apollo Client for handling GraphQL queries and mutations efficiently in the frontend.

2. **Backend (API Layer):**
   - **GraphQL API:** A GraphQL API layer built to interact with the Supabase backend. This allows the frontend to fetch specific data tailored to its needs, improving performance and reducing data overhead.
   - **Authentication:** Managed via Supabase's built-in authentication services, which support various authentication methods (e.g., email/password, OAuth providers).
   - **Real-Time Data Management:** Supabase's real-time capabilities are used to keep the user's fridge inventory, shopping lists, and other dynamic data synchronized across devices.

3. **Database and Storage:**
   - **Database:** Supabase (PostgreSQL) serves as the primary database, storing all user data, including profiles, inventory, nutritional information, and shopping lists.
   - **Storage:** Supabase also provides storage solutions for handling media files, such as product images, scanned documents, or AR models used in the fridge management feature.

4. **External Integrations:**
   - **Nutrition Data API:** Integrated with external nutrition data providers (e.g., USDA, FatSecret) via GraphQL to fetch and display detailed nutritional information about food products.
   - **Price Comparison API:** Connected to various price comparison services (e.g., RapidAPI, PriceAPI) through GraphQL, enabling real-time price comparisons across multiple retailers.
   - **Barcode/QR Code Scanning SDK:** Utilized for inventory management, allowing users to scan products directly into their fridge inventory.
   - **Voice Assistant SDK:** Integrated with Alexa and Google Assistant to enable voice commands for adding items to shopping lists, checking inventory, and more.

5. **Deployment:**
   - **Frontend Deployment:** The frontend application is deployed using platforms like Vercel or Netlify, which offer seamless integration with React.js and Tailwind CSS, ensuring fast and reliable hosting.
   - **Backend Deployment:** Supabase handles the backend infrastructure, providing managed services for the PostgreSQL database, authentication, and real-time APIs.

#### **System Architecture Diagram:**



### **Key Enhancements:**
- **Supabase Integration:** Leveraging Supabase for real-time data synchronization, PostgreSQL database management, and authentication simplifies backend development and ensures scalability.
- **GraphQL API:** The use of a GraphQL API enhances flexibility in data retrieval, allowing the frontend to request exactly the data it needs and nothing more, improving performance.
- **Tailwind CSS:** Provides a utility-first approach to styling, enabling rapid UI development and ensuring a consistent, responsive design across all devices.

This updated architecture is well-suited for modern web applications, ensuring that MARCO is scalable, maintainable, and capable of delivering a smooth and responsive user experience.



### Storage/Persistent Data Strategy
- **User Data:** Stored in MongoDB, including profiles, preferences, dietary goals, and shopping history.
- **Inventory Data:** Also stored in MongoDB, tracking quantities, expiration dates, and nutritional content of each product in the user's fridge.
- **Session Data:** Managed using Redis for quick access and to handle user sessions securely.

### Noteworthy Trade-offs and Choices
- **Technology Stack:** We chose MongoDB for its flexibility in handling diverse data structures (like nutrition data and shopping lists). Node.js with Express.js was selected for its performance and ease of integration with frontend frameworks.
- **Real-time vs. Batch Processing:** Real-time updates for inventory management and shopping list generation were prioritized to enhance user experience. However, some analytics functions are processed in batches to optimize performance.
- **Mobile-First Design:** The UI/UX design prioritizes mobile users, given the nature of grocery shopping, though full functionality is maintained on web platforms.

### Concurrent Processes
- **Real-Time Inventory Management:** Synchronization of fridge inventory updates with user actions, managed via WebSockets to ensure data consistency across devices.
- **Background Price Comparison:** Regular updates on product prices across different stores, processed in the background to provide up-to-date information without affecting user experience.

### Package Diagram


## Data Definitions

| Field/Attribute | Type       | Meaning                                               | Example                    |
|-----------------|------------|-------------------------------------------------------|----------------------------|
| userId          | String     | Unique identifier for each user                        | "user12345"                |
| userName        | String     | User's name                                            | "John Doe"                 |
| email           | String     | User's email address                                   | "john.doe@example.com"     |
| dietaryGoals    | Object     | User's dietary goals (e.g., daily calorie intake)      | {"calories": 2000, "protein": 150} |
| productId       | String     | Unique identifier for each product                     | "product12345"             |
| productName     | String     | Name of the product                                    | "Whole Milk"               |
| macros          | Object     | Nutritional content (proteins, carbs, fats) of product | {"protein": 8, "carbs": 12, "fats": 8} |
| quantity        | Number     | Quantity of the product in the fridge                  | 1.5 (liters)               |
| expirationDate  | Date       | Expiration date of the product                         | "2024-08-30"               |
| price           | Number     | Price of the product at a specific store               | 3.49 (USD)                 |
| storeName       | String     | Name of the store offering the product                 | "Walmart"                  |

---

## Analysis and Design

### Class Diagram


### State Diagrams

#### FoodProduct State Diagram


## Requirements Traceability Matrix

| Requirement-ID  | Use Cases            | Classes           | Methods                | Packages                |
|-----------------|----------------------|-------------------|------------------------|-------------------------|
| REQ-01          | User Authentication   | User              | authenticate()         | User Interface          |
| REQ-02          | Manage Inventory      | FridgeInventory   | addProduct(), removeProduct() | Inventory Management  |
| REQ-03          | Track Nutrition       | FoodProduct       | getProductInfo()       | Nutrition & Macro Tracking |
| REQ-04          | Generate Shopping List| ShoppingList      | generateList()         | Shopping List Management |
| REQ-05          | Price Comparison      | PriceComparison   | comparePrices()        | Price Comparison        |

---

## List of Design Assumptions

1. **Mobile-First Approach:** The design prioritizes mobile usability, assuming the majority of users will access MARCO via smartphones.
2. **Single User per Account:** The system is designed for individual users managing their own inventories and shopping lists, without shared accounts.
3. **Real-Time Updates:** Inventory and price data are assumed to be updated in near real-time, relying on stable and frequent API calls.

---

## Test Specifications

### Test Case Specifications

| Test Case ID | Test Description                           | Input Specifications                       | Output Specifications                        |
|--------------|--------------------------------------------|--------------------------------------------|----------------------------------------------|
| TC-01        | User Authentication                        | Username, Password                         | Successful login, User profile loaded        |
| TC-02        | Add Product to Inventory                   | Product Name, Quantity, Expiration Date    | Product added to inventory                   |
| TC-03        | Generate

 Shopping List                     | Fridge Inventory, Dietary Goals            | Customized shopping list generated           |
| TC-04        | Compare Product Prices                     | Product Name                               | List of prices across different stores       |
| TC-05        | Track Nutritional Intake                   | FoodProduct info, Daily Goals              | Updated daily intake summary                 |

### Test Plan

- **Test Schedule:**
  - Week 1: User Interface Testing
  - Week 2: Inventory Management Testing
  - Week 3: Price Comparison and Nutrition Tracking Testing
  - Week 4: Integration Testing and Final Bug Fixing

- **Testing Resources Required:**
  - Test devices (smartphones, tablets)
  - Access to all APIs
  - Testing tools (e.g., Postman, Selenium)

- **Testing Milestones:**
  - Completion of UI Testing
  - Completion of Backend Functionality Testing
  - Final Integration and Acceptance Testing

- **Test Deliverables:**
  - Test Case Reports
  - Bug and Issue Logs
  - Final Test Summary Report

---

## Project Management

### Minimal Viable Product

The Minimal Viable Product (MVP) for MARCO includes the following features:
- User authentication and profile management
- Basic fridge inventory management
- Macro tracking and dietary goal setting
- Shopping list generation based on inventory and dietary goals
- Basic price comparison functionality

These features allow early adopters to manage their kitchen inventory, track their nutrition, and generate shopping lists, providing immediate value and allowing for initial feedback collection.

### Milestones

1. **Milestone 1: System Setup and Basic Functionality**
   - Setup of the development environment
   - User authentication and profile management

2. **Milestone 2: Inventory Management and Macro Tracking**
   - Implementation of fridge inventory management
   - Macro tracking and dietary goal setting

3. **Milestone 3: Shopping List Generation and Price Comparison**
   - Shopping list generation
   - Price comparison functionality

4. **Milestone 4: Integration and User Interface Finalization**
   - Integration of all modules
   - Finalization of UI/UX

5. **Milestone 5: Testing and Deployment**
   - Comprehensive testing of all features
   - Deployment of the MVP

### Tasks

| Task ID | Task Description                         | Dependencies            | Effort | Milestone     |
|---------|------------------------------------------|-------------------------|--------|---------------|
| T1      | Set up development environment           | None                    | S      | Milestone 1   |
| T2      | Implement user authentication            | T1                      | M      | Milestone 1   |
| T3      | Develop fridge inventory management      | T2                      | M      | Milestone 2   |
| T4      | Implement macro tracking                 | T3                      | L      | Milestone 2   |
| T5      | Create shopping list generation feature  | T4                      | M      | Milestone 3   |
| T6      | Implement price comparison functionality | T5                      | L      | Milestone 3   |
| T7      | Finalize UI/UX design                    | T6                      | M      | Milestone 4   |
| T8      | Conduct integration testing              | T7                      | L      | Milestone 5   |
| T9      | Deploy MVP                               | T8                      | S      | Milestone 5   |

### Risks

| Risk ID | Description                                             | Probability | Severity | Mitigation Strategy                         |
|---------|---------------------------------------------------------|-------------|----------|---------------------------------------------|
| R1      | Changes in user requirements                            | Medium      | High     | Regular stakeholder meetings and feedback   |
| R2      | API availability issues (e.g., price comparison, nutrition) | Low         | High     | Implement fallback mechanisms               |
| R3      | Performance issues during peak usage                    | Medium      | Medium   | Optimize code and use scalable cloud services|
| R4      | Dependency on external data accuracy (e.g., nutrition data) | Low         | Medium   | Cross-check with multiple data sources      |
| R5      | Delays in integration of AR features                    | Medium      | Medium   | Prioritize AR as a later phase development  |

---

## Summary and Outlook

MARCO aims to transform the grocery shopping experience by integrating smart shopping, nutrition tracking, and inventory management into a single, user-friendly platform. By focusing on the user's dietary goals and providing actionable insights, MARCO helps users make healthier and more cost-effective choices, while reducing food waste. As the project progresses, future developments may include expanded integrations with fitness apps, enhanced AI-driven recommendations, and support for additional smart kitchen devices.



## Appendices

- **Log of Interactions with Stakeholders**
  - Meeting on [Date]: Discussed core features and MVP scope with stakeholders.
  - Meeting on [Date]: Reviewed system architecture and data strategy.
  - Meeting on [Date]: Finalized UI/UX design considerations.

- **References**
  - [MongoDB Documentation](https://docs.mongodb.com/)
  - [Node.js Documentation](https://nodejs.org/en/docs/)
  - [React.js Documentation](https://reactjs.org/docs/getting-started.html)

- **Third-party Resources**
  - Nutrition API (USDA, FatSecret)
  - Price Comparison API (RapidAPI, PriceAPI)
  - Barcode/QR Code Scanning SDK (ZXing, Dynamsoft)
  - Voice Assistant SDKs (Alexa, Google Assistant)
  - AR SDKs (AR.js, Vuforia)

---

