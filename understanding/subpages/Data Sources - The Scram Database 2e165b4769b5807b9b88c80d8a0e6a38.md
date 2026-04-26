# Data Sources - The Scram Database

The **Scram Database** is a built-in **PostgreSQL database** that comes with every Scram app. It's your app's persistent data storage, where all your application data resides. T

---

## 🗄️ **Key Features**

### **PostgreSQL-Powered**

- Full-featured relational database with SQL support
- ACID compliant (reliable, safe transactions)
- Supports complex queries, joins, indexes, and constraints
- 30-second query timeout for safety

### **Automatic Table Structure**

Every table automatically includes:

- **`id`** field (UUID primary key) - unique identifier for each row
- Automatic timestamps and metadata tracking
- Case-sensitive naming: Tables use **PascalCase** (`Users`, `Products`), fields use **camelCase** (`firstName`, `createdAt`)