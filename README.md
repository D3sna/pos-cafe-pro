rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    // Aturan global: Mengizinkan akses baca dan tulis ke semua dokumen.
    // Ini sangat berguna untuk tahap pengembangan agar sinkronisasi antar HP lancar.
    match /{document=**} {
      allow read, write: if true;
    }

    // Aturan spesifik untuk struktur data aplikasi (opsional namun menambah stabilitas).
    match /artifacts/{appId}/public/data/{collectionName}/{docId} {
      allow read, write: if true;
    }
  }
}
