# Configuración de QA del proyecto
> Copia este archivo a la raíz del repo que vas a probar y ajusta los valores.

## Gestor de historias
- Herramienta: Jira | Azure DevOps | GitHub Issues | Linear
- Acceso: conector MCP (recomendado) | página pública

## Backend
- Stack: Java 17, Spring Boot 3, PostgreSQL, Flyway
- Pruebas unitarias / integración: JUnit 5 + Spring Boot Test + MockMvc / RestAssured
- Ruta de pruebas: `backend/src/test/java/`
- Comando (pruebas específicas): `cd backend && mvn -q test -Dtest=<Clases>`
- BD de pruebas: Testcontainers (PostgreSQL 16)
- Perfil de Spring para pruebas: `test`

## Frontend
- Stack: React 18 + Vite
- Unitarias: Vitest + @testing-library/react — `frontend/src/**/*.test.tsx`
- Comando: `cd frontend && npx vitest run <archivos>`
- E2E: Playwright — `e2e/tests/`
- Comando: `cd e2e && npx playwright test <archivos>`
- URL base: `http://localhost:5173`
- Cómo levantar la app para e2e: `docker compose up -d` o `mvn spring-boot:run` + `npm run dev`

## Autenticación para pruebas
- Usuarios de prueba (semilla Flyway de perfil `test`): `qa-admin`, `qa-user`
- Contraseñas: variables de entorno `QA_ADMIN_PASSWORD`, `QA_USER_PASSWORD`

## CI
- Plataforma: GitHub Actions — `.github/workflows/`

## Cumplimiento aplicable
- Maneja datos personales: Sí / No
- Maneja datos de salud: Sí / No
