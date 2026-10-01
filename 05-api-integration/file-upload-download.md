# File Upload, Image Upload & Downloads

## 1. Concept (Hinglish)
Upload: `FormData` + `multipart/form-data`. Download: `responseType: 'blob'`.

## 2. Why do we need it?
Profile image, documents, reports (CSV/PDF) HRMS me common hain.

## 3. Laravel Comparison
`$request->file('avatar')->store('avatars','public')` aur `Storage`. `php artisan storage:link`. Frontend side naya hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Base64 JSON me bhejna (heavy).

## 5. Syntax
```jsx
// upload
const fd = new FormData();
fd.append("name", form.name);
if (file) fd.append("avatar", file);
await api.post("/employees", fd); // Content-Type browser boundary ke saath khud set karta hai
// update with file (Laravel PUT/PATCH multipart issue)
fd.append("_method", "PUT"); await api.post(`/employees/${id}`, fd);

// preview
const url = URL.createObjectURL(file);   // cleanup: URL.revokeObjectURL(url)

// download
const res = await api.get("/employees/export", { responseType: "blob" });
const a = document.createElement("a");
a.href = URL.createObjectURL(res.data); a.download = "employees.csv"; a.click();
```
```php
$path = $request->file('avatar')->store('avatars', 'public');
return Storage::disk('public')->download($path);
```

## 6. Example
Multiple files: `files.forEach(f => fd.append("documents[]", f))`; Laravel rule `documents.*` => `file|max:5120`.

## 7. Internal Working
Browser multipart body banata hai; Content-Type header manually set mat karo (boundary missing ho jaayega).

## 8. Animation / Flow
```text
select file -> FormData -> multipart POST -> Laravel validate -> store -> path DB -> URL response
```

## 9. When to use
Images/docs upload.

## 10. When NOT to use
Bahut bade files (chunked/direct-to-S3 pre-signed URL).

## 11. Alternatives
Pre-signed S3 uploads, chunk upload.

## 12. Why this approach / Trade-offs
FormData native aur simple.

## 13. Common Mistakes
Content-Type manually set, PUT + multipart Laravel issue, file size/type validate sirf frontend, memory leak (ObjectURL revoke).

## 14. Best Practices
Server validation (`image|max`), preview, progress (`onUploadProgress`).

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- File upload kaise?
- PUT me file Laravel me kyun nahi aati?
- Blob download kaise?

## 18. Interview English Answer
> I send files with FormData as multipart requests, validate type and size on the Laravel side, and for downloads I request a blob and trigger a temporary object URL.

## 19. Practical Task (solution pehle khud try karo)
Profile image upload (preview + progress) aur employees CSV export banao.

## 20. Revision Points
- FormData
- _method=PUT spoof
- Blob download

