# Pyro Backend - API de Gestión de Habitaciones de Motel

API REST desarrollada con FastAPI para la gestión de habitaciones del Motel Pyro. Permite registrar, consultar, actualizar y liberar habitaciones de manera eficiente.

## 🚀 Características

- **FastAPI**: Framework moderno y rápido para APIs REST
- **Validación automática**: Usando Pydantic para validación de datos
- **CORS configurado**: Para permitir requests desde el frontend
- **Documentación automática**: Swagger UI disponible en `/docs`
- **Gestión de impuestos**: Cálculo automático de ISH (4%) e IVA (16%)
- **Modo memoria**: Para desarrollo y testing sin persistencia

## 📋 Requisitos

- Python >= 3.13
- Poetry (para gestión de dependencias)

## 🛠️ Instalación

1. **Instalar dependencias con Poetry:**
   ```bash
   poetry install --no-root
   ```

2. **Activar el entorno virtual (opcional):**
   ```bash
   poetry shell
   ```

## 🚀 Ejecución

### Ejecutar con Poetry (Recomendado):
```bash
poetry run uvicorn main:app --reload
```

### Ejecutar directamente:
```bash
poetry shell
uvicorn main:app --reload
```

La API estará disponible en: `http://localhost:8000`

## 📚 Documentación

- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

## 🔗 Endpoints de la API

### Información General
- `GET /` - Información básica de la API
- `GET /health` - Verificación de salud del servicio

### Gestión de Habitaciones
- `POST /rooms` - Registrar nueva habitación
- `GET /rooms` - Obtener todas las habitaciones activas
- `GET /rooms/history` - Obtener historial completo de habitaciones
- `GET /rooms/{room_id}` - Obtener habitación por ID
- `GET /rooms/number/{room_number}` - Obtener habitación por número
- `PUT /rooms/{room_number}` - Actualizar habitación
- `DELETE /rooms/{room_id}` - Hacer checkout por ID
- `DELETE /rooms/number/{room_number}` - Hacer checkout por número
- `DELETE /rooms` - Liberar todas las habitaciones

## 📝 Modelos de Datos

### RoomCreate (Crear habitación)
```json
{
  "roomType": "Sencilla" | "Jacuzzi",
  "basePrice": 100.0,
  "hours": 3,
  "roomNumber": "101",
  "guestPlates": "ABC123",
  "guestModel": "Toyota Corolla",
  "guestId": "12345678"
}
```

### Room (Respuesta completa)
```json
{
  "id": 1,
  "roomType": "Sencilla",
  "basePrice": 100.0,
  "hours": 3,
  "roomNumber": "101",
  "guestPlates": "ABC123",
  "guestModel": "Toyota Corolla",
  "guestId": "12345678",
  "roomRegisterTime": "2025-06-27 14:30:00",
  "ISH": 4.0,
  "IVA": 16.0,
  "totalPrice": 120,
  "isActive": true
}
```

## 💰 Cálculo de Precios

El sistema calcula automáticamente:
- **ISH (Impuesto sobre Hospedaje)**: 4% del precio base
- **IVA**: 16% del precio base
- **Precio Total**: Precio base + ISH + IVA

Ejemplo:
- Precio base: $100
- ISH: $4 (4%)
- IVA: $16 (16%)
- **Total: $120**

## 🏗️ Estructura del Proyecto

```
backend-apppyro/
├── main.py           # Aplicación principal FastAPI
├── models.py         # Modelos Pydantic
├── service.py        # Lógica de negocio
├── pyproject.toml    # Configuración Poetry
├── requirements.txt  # Dependencias
└── README.md         # Este archivo
```

## 🔧 Configuración

### Modo Memoria
Por defecto, la aplicación funciona en modo memoria (`memory_only=True`), lo que significa:
- No se persisten datos entre reinicios
- Ideal para desarrollo y testing
- Rendimiento más rápido

### CORS
Configurado para permitir requests desde cualquier origen (`allow_origins=["*"]`). En producción, especificar dominios específicos.

## 🧪 Testing

Para probar la API, puedes usar:
- **Swagger UI**: `http://localhost:8000/docs`
- **curl**: Comandos de terminal
- **Postman**: Herramienta de testing de APIs
- **Frontend**: La aplicación web incluida en este proyecto

### Ejemplo con curl:
```bash
# Crear habitación
curl -X POST "http://localhost:8000/rooms" \
  -H "Content-Type: application/json" \
  -d '{
    "roomType": "Sencilla",
    "basePrice": 100.0,
    "hours": 3,
    "roomNumber": "101",
    "guestPlates": "ABC123",
    "guestModel": "Toyota Corolla",
    "guestId": "12345678"
  }'

# Obtener todas las habitaciones
curl -X GET "http://localhost:8000/rooms"
```

## 🤝 Integración con Frontend

Esta API está diseñada para trabajar con el frontend del Motel Pyro. El frontend consume estos endpoints para:
- Mostrar habitaciones disponibles y ocupadas
- Registrar nuevas habitaciones
- Gestionar check-in y check-out
- Mostrar historial de habitaciones

## 📄 Licencia

Proyecto desarrollado para Motel Pyro.

## 👨‍💻 Desarrollador

- **Autor**: Forek4st
- **Email**: janeirojm91@gmail.com

---

Para más información o soporte, contacta al desarrollador.
