# School Management System Django API

## Setup

1. Create virtual environment (optional):

```bash
python -m venv venv
source venv/bin/activate  # Linux/MacOS
venv\Scripts\activate   # Windows
```

2. Install dependencies:

```bash
pip install django djangorestframework djangorestframework-simplejwt
```

3. Run migrations:

```bash
python manage.py makemigrations
python manage.py migrate
```

4. Create superuser:

```bash
python manage.py createsuperuser
```

5. Run server:

```bash
python manage.py runserver
```

## JWT API

- Obtain token:

POST `/api/token/`

Payload:

```json
{
  "username": "yourusername",
  "password": "yourpassword"
}
```

- Refresh token:

POST `/api/token/refresh/`

Payload:

```json
{
  "refresh": "<refresh_token>"
}
```

- Use access token:

Set header

```
Authorization: Bearer <access_token>
```

- Example API endpoints:

```
GET /api/students/
GET /api/workers/
```

---

## Permissions

- Students API allowed for groups: Admin, Staff  
- Workers API allowed for group: Admin  
- Superusers bypass permissions

---

## Admin

Use admin panel to create groups and assign users:

http://localhost:8000/admin/

---

## New API Endpoints & Examples

### Kitchen Inventory

- List items:
  ```
  curl -H "Authorization: Bearer <access_token>" http://localhost:8000/api/kitchen-items/
  ```

- Add item:
  ```
  curl -X POST http://localhost:8000/api/kitchen-items/ \
   -H "Authorization: Bearer <access_token>" \
   -H "Content-Type: application/json" \
   -d '{"name":"Rice", "quantity":50, "unit":"kg"}'
  ```

### Hostel Rooms

- List rooms:
  ```
  curl -H "Authorization: Bearer <access_token>" http://localhost:8000/api/hostel-rooms/
  ```

- Add room:
  ```
  curl -X POST http://localhost:8000/api/hostel-rooms/ \
   -H "Authorization: Bearer <access_token>" \
   -H "Content-Type: application/json" \
   -d '{"room_number":"A101", "capacity":3}'
  ```

### Hostel Bookings

- List bookings:
  ```
  curl -H "Authorization: Bearer <access_token>" http://localhost:8000/api/hostel-bookings/
  ```

- Add booking:
  ```
  curl -X POST http://localhost:8000/api/hostel-bookings/ \
   -H "Authorization: Bearer <access_token>" \
   -H "Content-Type: application/json" \
   -d '{"student":1, "room":1, "check_in":"2025-05-15", "check_out":"2025-06-15"}'
  ```

---

## New Groups to create:

- KitchenStaff
- HostelManager

Assign users accordingly to control access.
