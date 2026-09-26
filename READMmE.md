RideCash v2 — cash ride-hailing MVP
This version adds OTP verification, driver KYC workflow, points + nearest-driver matching, real-time Socket.IO ride events, background driver location, push-token storage, safety reporting, commission debt/lockout, admin KYC approval and commission settlement endpoints.
Stack
Mobile: Expo React Native + react-native-maps + expo-location + expo-notifications + Socket.IO client
Backend: Node.js + Express + TypeScript + Socket.IO
Database: PostgreSQL + Prisma
Cash/12% rule
Passenger pays driver cash. A completed ride has commission = round(fare * 0.12). The admin settlement endpoint adds this amount to the driver's commission debt. Driver cannot go online or accept rides when KYC is not approved or debt is above the configured limit.
Setup backend
cd backend
copy .env.example to .env and set DATABASE_URL/JWT_SECRET
npm install
npx prisma generate
npx prisma migrate dev --name init
npm run seed
npm run dev
Demo admin: 255700000000 / ChangeMe123! Demo driver: 255711111111 / ChangeMe123! Change these credentials immediately outside development.
Setup mobile
cd mobile
npm install
copy .env.example to .env and set your computer LAN IP, e.g. http://192.168.1.10:4000/api
npx expo start
For a real Android/iOS build, configure Maps keys and production HTTPS. Background location and push notifications require a development/production build; Expo Go has platform limitations.
Production items still required before launch
Real SMS OTP provider and rate limiting
Real KYC document storage/object storage and admin review UI
Secure push notifications via Expo/FCM/APNs
HTTPS, secrets manager, database backups and monitoring
Anti-fraud, ride cancellation policy, driver identity verification and audit logs
Tanzania legal/business compliance, privacy policy and terms
Production payment provider for driver commission settlement (ClickPesa/Selcom can be plugged into the settlement service)
Proper emergency/safety operations and human support
