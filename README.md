# 🤖 3-DOF Robotic Arm: Design, Math & Control

![Robot Demo](media/demo.gif) <!-- Taruh GIF gerak robot atau render 3D di paling atas -->

Projek ini adalah perancangan robot manipulator 3-DOF (Degree of Freedom) berbasis motor servo. Fokus utama projek ini mencakup perancangan mekanik, kalkulasi torsi, pemodelan **Forward & Inverse Kinematics**, hingga integrasi kontrol pergerakan secara real-time.

---

## 📌 Spesifikasi Utama
- **Derajat Kebebasan (DOF):** 3 (Base Yaw, Shoulder Pitch, Elbow Pitch)
- **Konfigurasi Sendi:** 
  - Joint 1 (Base): Yaw ($\theta_1$)
  - Joint 2 (Bahu): Pitch 1 ($\theta_2$)
  - Joint 3 (Siku): Pitch 2 ($\theta_3$)
- **Aktuator:** Servo MG996R (Bahu) & MG90S (Base & Siku)
- **Panjang Link:** $L_1 = 12\text{ cm}$, $L_2 = 10\text{ cm}$
- **Mikrokontroler:** ESP32 / Arduino

---

## 📐 Pemodelan Kinematika

### 1. Forward Kinematics (FK)
Menghitung posisi ujung lengan $(X, Y, Z)$ dari sudut tiap servo $(\theta_1, \theta_2, \theta_3)$:
$$r = L_1 \cos(\theta_2) + L_2 \cos(\theta_2 + \theta_3)$$
$$Z = L_1 \sin(\theta_2) + L_2 \sin(\theta_2 + \theta_3)$$
$$X = r \cos(\theta_1), \quad Y = r \sin(\theta_1)$$

### 2. Inverse Kinematics (IK)
Menghitung sudut $(\theta_1, \theta_2, \theta_3)$ berdasarkan koordinat tujuan $(X, Y, Z)$ menggunakan pendekatan geometris dan Hukum Kosinus:
$$\theta_1 = \text{atan2}(Y, X)$$
$$\cos(\gamma) = \frac{L_1^2 + L_2^2 - D^2}{2 \cdot L_1 \cdot L_2} \implies \theta_3 = 180^\circ - \gamma$$

*(Penurunan rumus lengkap & analisis batas workspace tersedia di folder `docs/`)*

---

## 🔌 Sistem Elektronika & Skematik

| Komponen | Spesifikasi | Fungsi |
| :--- | :--- | :--- |
| Servo Bahu | High Torque Metal Gear (MG996R) | Menahan beban statis & dinamis lengan |
| Servo Base & Siku | Micro Servo (MG90S) | Rotasi yaw dasar & tekukan siku |
| Power Supply | Adaptor 5V / 3A-5A | Sumber daya eksternal servo (Common Ground ke MCU) |

---

## 📸 Progres Pengerjaan
- [x] Kalkulasi Torsi Statis & Pemilihan Aktuator
- [x] Pemodelan Matematika Forward & Inverse Kinematics
- [ ] Desain CAD 3D & Simulasi Mekanik
- [ ] Wiring Hardware & Kalibrasi Sinyal PWM
- [ ] Pengujian Pergerakan Trajectory

---

## 🚀 Cara Menjalankan Kode
1. Clone repositori ini:
   ```bash
   git clone [https://github.com/username/3dof-robot-arm.git](https://github.com/username/3dof-robot-arm.git)
