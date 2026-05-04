Promt:
Role: You are an elite Full-Stack Creative Developer specializing in Interactive Computer Vision and Generative Art. Your goal is to engineer a high-performance Web AR application that merges MediaPipe's hand tracking with a high-fidelity visual and auditory experience.
Objective: Create a single-file (HTML/CSS/JS) production-ready application called "NEON AURA AR". The code must be clean, modular, and optimized for 60FPS.
Technical Blueprint:

1.	Frontend & UI Design:
o	Glassmorphism HUD: Implement a dashboard using CSS backdrop-filter: blur(). Include real-time stats for "Hands Detected", "FPS Counter", "Gesture State", and "Spread Percentage". 
o	Theme Engine: Create a system-wide theme manager with 5 presets (Rainbow, Cyberpunk, Lava, Ocean, Galaxy). All UI accents and canvas stroke colors must react to this central theme state. 
o	Responsiveness: Use a robust resize() handler to ensure the canvas fills the viewport perfectly and handles window scaling. 

2.	Visual Processing (The Dual-Canvas Engine):
o	Layer 1 (Background): A generative "Matrix Rain" or "Cyber-Grid" effect. The character falling speed must be a function of the hand's spatial velocity ($v = \Delta d / \Delta t$). 
o	Layer 2 (Foreground): High-intensity neon rendering. Utilize ctx.shadowBlur for bloom and ctx.globalCompositeOperation = 'screen' to create additive color blending where hand skeletons overlap. 
o	Motion Trails: Implement a "ghosting" effect using a semi-transparent destination-out fill on each frame instead of a full clearRect, creating a smooth visual decay for hand movements. 

3.	Interaction Physics & Gestures:
o	Gesture Engine: Program a proximity-based "Pinch" detector (Thumb + Index distance < 0.05). On pinch, trigger a radial shockwave using an easing function for expansion and alpha decay. 
o	Dynamic Particles: Emit spark particles from all 5 fingertips. Particles must have gravity and a lifespan. 
o	Multi-Hand Synergy: When two hands are detected:
	Draw high-frequency "Electric Arcs" between corresponding fingertips if they are within a certain distance threshold. 
	Calculate a centroid point between both hands to render a rotating generative "Mandala" wireframe. 

4.	Audio Synthesis (Web Audio API):
o	Initialize an AudioContext only after a user gesture (Start Overlay). 
o	Harmonic Hum: Use an oscillator to create a continuous drone. Modulate the frequency ($Hz$) and Gain based on the distance between index fingers to create a "Theremin" effect. 
o	Action SFX: Synthesize a percussive "Zap" sound (sawtooth wave with rapid exponential frequency ramp) whenever a pinch gesture is triggered. 

5.	MediaPipe Configuration:
o	Set modelComplexity: 1 and minDetectionConfidence: 0.7 to ensure stability. 
o	Use the official Google CDN for all @mediapipe dependencies. 
Output Requirement:
Produce the complete, unminified source code in one block. Ensure the JavaScript uses ES6+ features and includes comments explaining the mathematical logic used for the physics and audio modulations.


Alur Logika:
Alur Logika Sistem (Step-by-Step)
1.	Inisialisasi Lingkungan (Environment Setup): Aplikasi memuat library MediaPipe (Hands, Camera, Drawing Utils) dari CDN dan menyiapkan elemen video serta dua buah canvas (latar belakang dan latar depan) dengan sistem koordinat yang disesuaikan dengan ukuran layar pengguna. 
2.	Aktivasi Sensor & Audio: Sistem meminta izin akses kamera dan menginisialisasi AudioContext. Logika suara disetel pada kondisi silent (diam) sampai pengguna melakukan interaksi pertama (mengklik tombol start) untuk mematuhi kebijakan keamanan browser. 
3.	Pengambilan Frame Video: Kamera menangkap gambar secara real-time, lalu aplikasi melakukan mirroring (pembalikan horizontal) pada elemen video dan canvas agar gerakan tangan di layar sesuai dengan gerakan asli pengguna di dunia nyata. 
4.	Deteksi AI (Hand Tracking): Setiap frame dikirim ke model AI MediaPipe yang akan mengekstraksi 21 titik koordinat (landmarks) tangan dalam ruang 3D. AI ini memberikan data berupa koordinat $X, Y, Z$ yang dinormalisasi (0 hingga 1). 
5.	Pemetaan Koordinat (Mapping): Aplikasi mengubah koordinat normalisasi dari AI menjadi koordinat piksel aktual berdasarkan lebar dan tinggi layar browser agar visual neon tepat berada di atas posisi tangan asli. 
6.	Kalkulasi Kecepatan (Velocity): Sistem membandingkan posisi tangan pada frame saat ini dengan frame sebelumnya untuk mendapatkan nilai kecepatan ($v = \Delta d / \Delta t$). Nilai ini digunakan untuk mengatur seberapa cepat efek Matrix Rain jatuh di latar belakang. 
7.	Logika Gestur (Interaction Engine):
•	Pinch: Menghitung jarak Euclidean antara landmark ujung ibu jari dan ujung telunjuk. Jika jarak di bawah ambang batas tertentu, sistem memicu suara "Zap" dan efek visual ledakan. 
•	Spread: Menghitung jarak antar jari luar untuk menentukan apakah tangan sedang mengepal atau terbuka, yang kemudian ditampilkan pada HUD statis. 
8.	Pemrosesan Visual Berlapis (Rendering):
•	Background Layer: Menggambar karakter generatif yang kecepatannya mengikuti gerak tangan. 
•	Foreground Layer: Menggunakan mode screen untuk menciptakan efek pendaran cahaya (bloom) pada tulang tangan dan partikel di ujung jari. 
9.	Efek Jejak Cahaya (Motion Trails): Bukannya menghapus canvas di setiap frame, aplikasi menimpa frame lama dengan lapisan hitam transparan (destination-out), sehingga gerakan tangan meninggalkan jejak cahaya yang memudar perlahan. 
10.	Modulasi Suara Real-time: Jika terdeteksi dua tangan, aplikasi menghitung jarak di antaranya. Jarak ini dikonversi menjadi frekuensi hertz ($Hz$) pada osilator audio, menciptakan efek suara Theremin yang berubah nadanya saat tangan digerakkan menjauh atau mendekat. 
11.	Update HUD & Loop: Semua data (FPS, jumlah tangan, jenis gestur) diperbarui pada tampilan antarmuka (HUD) dan siklus kembali ke poin nomor 3 untuk frame berikutnya. 


