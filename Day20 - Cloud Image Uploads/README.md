# Day 20 — Cloud Image Uploads ☁️

## Project Repository

🔗 [File Uploads — GitHub](https://github.com/Greycode009/File-Uploads)

## Today's Progress

- Learned **cloud storage** for backend file uploads
- Switched to **Multer `memoryStorage()`**
- Uploaded images directly to **Supabase Storage**
- Generated and used **public image URLs**
- Connected the frontend with **cloud-hosted images**

## What I Learned

Today I moved from local file storage to a **production-style cloud storage workflow**.

I learned how Multer can keep uploaded files in memory using `memoryStorage()`, allowing the file buffer to be sent directly to Supabase Storage instead of saving it permanently on the server.

I also learned how to generate a public URL from Supabase Storage and use that URL to display the uploaded image on the frontend.

## Technologies

- Node.js
- Express.js
- Multer
- Supabase Storage
- JavaScript
- HTML/CSS/JavaScript

## Status

**Day 20 Complete ✅**

### Next

Continue with **advanced file uploads, storage management, and security**.