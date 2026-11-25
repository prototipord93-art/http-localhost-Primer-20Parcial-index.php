# PRESTANOVA

Plataforma SaaS multiempresa para administrar préstamos y operaciones financieras. La solución se construye por fases; esta carpeta contiene la fundación del backend Laravel y la estructura prevista de las aplicaciones.

## Estado de la primera etapa

- Backend creado con Laravel 13.44.1 y PHP 8.3.
- API preparada con Laravel Sanctum; las rutas usan el prefijo `/api/v1`.
- Dependencias PHP instaladas y fijadas en `backend/composer.lock`.
- Migraciones base de Laravel y Sanctum aplicadas en la SQLite local.
- La prueba de instalación de Laravel pasa con SQLite en memoria.
- No están implementados todavía el registro, las empresas ni los módulos financieros.

## Estructura inicial

```text
PRESTANOVA/
├── backend/                 # Laravel: API REST y panel Blade
│   ├── app/                  # Modelos, controladores, servicios y políticas
│   ├── database/migrations/  # Esquema base y migraciones futuras por módulo
│   ├── resources/views/      # Panel web Laravel Blade
│   ├── routes/               # Rutas web y API versionada
│   └── tests/                # Pruebas de backend
├── mobile/                  # Aplicación Flutter (estructura preparada)
├── web/                     # Nota de arquitectura; el panel vive en backend/
├── docs/                    # Arquitectura, datos, reglas, seguridad y despliegue
└── infrastructure/          # Directorios previstos para despliegue y operación
```

La interfaz web se implementará dentro de Laravel (`backend/resources/views`, `backend/resources/css` y `backend/resources/js`). No se mantiene un segundo frontend web separado porque la tecnología acordada es Blade.

## Requisitos locales

- PHP 8.3 con `bcmath`, `curl`, `dom`, `fileinfo`, `mbstring`, `openssl`, `pdo_mysql`, `tokenizer` y `xml` habilitados.
- Composer 2.
- MySQL 8 o compatible para trabajar con datos persistentes.
- Node.js y npm para compilar los recursos web de Laravel.
- Flutter y Dart para comenzar la aplicación móvil.

En esta estación se detectó PHP 8.3.1 en MAMP y un servidor MySQL 5.7.24 activo. Laravel 13 admite MySQL 5.7+, aunque PRESTANOVA apunta a MySQL 8. No se pudo autenticar contra el servidor con el usuario `root` sin contraseña, por lo que las migraciones se probaron con SQLite. Flutter y Composer no estaban disponibles en `PATH`. Composer 2.11.3 se descargó a una ubicación temporal solo para crear este backend.

## Configuración del backend

Laravel utiliza `backend/.env`; `backend/.env.example` es su plantilla. El `.env.example` de la raíz contiene únicamente valores compartidos del proyecto.

```powershell
Set-Location backend
composer install
Copy-Item .env.example .env
php artisan key:generate
```

Configura en `backend/.env` la conexión a una instancia MySQL 8 local antes de ejecutar migraciones persistentes. No pongas secretos reales en archivos versionados.

Para ejecutar las pruebas del backend:

```powershell
Set-Location backend
php artisan test
```

Las pruebas incluidas en esta etapa usan SQLite en memoria y no verifican compatibilidad con MySQL. Consulta [docs/deployment.md](docs/deployment.md) para los hallazgos del entorno MAMP y [docs/database.md](docs/database.md) para el plan de migraciones.

## Documentación

- [Arquitectura](docs/architecture.md)
- [Base de datos y migraciones](docs/database.md)
- [API](docs/api-endpoints.md)
- [Reglas de negocio](docs/business-rules.md)
- [Seguridad](docs/security.md)
- [Pantallas móviles](docs/mobile-screens.md)
- [Despliegue](docs/deployment.md)
- [Pruebas](docs/testing.md)

No comenzar la Fase 2 hasta revisar esta fundación y autorizar el avance.
