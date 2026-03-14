rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    // Aturan global untuk pengembangan: Mengizinkan akses ke semua dokumen
    // Pastikan jalur (path) ini sesuai dengan struktur yang digunakan di app.js
    match /{document=**} {
      allow read, write: if true;
    }

    // Aturan spesifik untuk aplikasi (opsional namun lebih stabil)
    match /artifacts/{appId}/public/data/{collectionName}/{docId} {
      allow read, write: if true;
    }
  }
}
