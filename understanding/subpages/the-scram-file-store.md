# The Scram File Store

Every Scram project has a **File Store** that is shared across the Apps in your Project.

 

The **Scram File Store** is a built-in cloud storage system in Scram that allows you to store and manage files for your application. Think of it as your app's file cabinet in the cloud - perfect for user uploads, images, documents, PDFs, and any other files your app needs to handle.

### Key Features:

**📁 File Storage**

- Store files in organised paths (like folders)
- Each file gets a unique `fileUri` identifier
- Supports any file type (images, PDFs, videos, documents, etc.)

**🔑 How It Works:**

The file store uses a **3-step upload process**:

1. **Prepare File Upload**
    - Request an upload URL for a file
    - Inputs: `path` (where to store), `contentType` (file MIME type)
    - Returns: `uploadUrl` (temporary URL) and `fileUri` (permanent identifier)
2. **Upload File To Url**
    - Send the actual file to the upload URL
    - Inputs: `file` (from user), `uploadToUrl` (from step 1)
    - Returns: Public URL to access the file
3. **List Files**
    - Browse files in a specific path
    - Input: `path` (folder to list)
    - Returns: Array of files with name, URI, size, and lastModified date

### Common Use Cases:

- 📸 **User profile photos**
    - Store avatars and profile images
- 📄 **Document management**
    - Upload and organize PDFs, contracts, invoices
- 🖼️ **Image galleries**
    - Photo collections, product images
- 📎 **Attachments**
    - Files attached to records (support tickets, messages)
- 🎨 **Media libraries**
    - Store and manage app assets