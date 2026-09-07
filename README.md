# FlexMobile Financing System

A comprehensive financing server for managing device financing, payments, and customer relationships with automated payment enforcement.

## System Architecture

```
FLEXMOBILE ADMIN
       │
       ▼
┌─────────────────┐
│ Financing Server│
└────────┬────────┘
         │
  ┌──────┼──────┐
  ▼      ▼      ▼
Customers Payments Devices
  │      │      │
  └──────┼──────┘
         ▼
  Payment Engine
         │
    ┌────┴────┐
    ▼         ▼
PAID/ACTIVE OVERDUE
              │
        Warning Sequence
              │
        Enforcement Rule
              │
              ▼
      Device Restriction
              │
       Payment Received
              │
              ▼
           UNLOCK
```

## Features

- **Customer Management**: Create and manage customer profiles
- **Device Management**: Track financed devices per customer
- **Payment Processing**: Handle payment transactions and status updates
- **Payment Engine**: Automatic payment status tracking
- **Warning System**: Send notifications for overdue payments
- **Enforcement Rules**: Automatic device restrictions for non-payment
- **Device Locking/Unlocking**: Restrict or unlock devices based on payment status

## Project Structure

```
flexmobile-financing-system/
├── src/
│   ├── models/
│   │   ├── Customer.js
│   │   ├── Device.js
│   │   └── Payment.js
│   ├── services/
│   │   ├── PaymentEngine.js
│   │   ├── PaymentService.js
│   │   ├── DeviceService.js
│   │   ├── CustomerService.js
│   │   └── EnforcementService.js
│   ├── routes/
│   │   ├── customers.js
│   │   ├── devices.js
│   │   └── payments.js
│   ├── middleware/
│   │   ├── auth.js
│   │   └── errorHandler.js
│   ├── database/
│   │   ├── connection.js
│   │   └── schema.sql
│   └── app.js
├── config/
│   └── config.js
├── tests/
│   ├── payment.test.js
│   ├── device.test.js
│   └── customer.test.js
├── .env.example
├── package.json
└── README.md
```

## Installation

1. Clone the repository
```bash
git clone https://github.com/matlerethejane6-cmd/flexmobile-financing-system.git
cd flexmobile-financing-system
```

2. Install dependencies
```bash
npm install
```

3. Set up environment variables
```bash
cp .env.example .env
```

4. Set up the database
```bash
node src/database/connection.js
```

5. Start the server
```bash
npm start
```

## API Endpoints

### Customers
- `POST /api/customers` - Create a new customer
- `GET /api/customers/:id` - Get customer details
- `PUT /api/customers/:id` - Update customer information
- `GET /api/customers` - List all customers

### Devices
- `POST /api/devices` - Register a new device
- `GET /api/devices/:id` - Get device details
- `PUT /api/devices/:id/restrict` - Restrict a device
- `PUT /api/devices/:id/unlock` - Unlock a device
- `GET /api/customers/:customerId/devices` - Get devices by customer

### Payments
- `POST /api/payments` - Process a payment
- `GET /api/payments/:id` - Get payment details
- `GET /api/payments/customer/:customerId` - Get customer payment history
- `POST /api/payments/:id/process` - Process pending payment

## Database Schema

See `src/database/schema.sql` for the complete database structure.

## Payment Flow

1. Customer registers with device
2. Payment is due on scheduled date
3. Payment Engine checks payment status
4. If PAID/ACTIVE - Device remains active
5. If OVERDUE:
   - Warning sequence is initiated
   - Enforcement rule is triggered
   - Device is restricted
   - Customer receives notifications
6. Upon payment receipt:
   - Payment status updated to PAID
   - Device is unlocked
   - Service restored

## Technologies

- Node.js / Express.js
- MySQL / PostgreSQL
- JWT Authentication
- RESTful API
- Jest (Testing)

## Environment Variables

```
PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=password
DB_NAME=flexmobile_financing
JWT_SECRET=your_secret_key
NODE_ENV=development
```

## Testing

```bash
npm test
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first.

## License

MIT License - see LICENSE file for details

## Support

For support, email support@flexmobile.com or open an issue on GitHub.
