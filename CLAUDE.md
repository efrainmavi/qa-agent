# Agente QA — convenciones del proyecto

Este proyecto define un sistema multi‑agente de QA que se lanza con:

```
/test <link-de-la-historia-de-usuario>
```

## Jerarquía
```
QA (comando /test — hilo principal)
├── analista                  (sub‑orquestador, secuencial)
│   ├── analista-requerimientos
│   └── analista-test-design
├── automatizador             (sub‑orquestador, ciclo coder→runner ≤3 veces)
│   ├── automatizador-coder
│   ├── automatizador-runner
│   └── automatizador-reporter
└── audit                     (sub‑orquestador, revisores en paralelo)
    ├── audit-code-reviewer
    ├── audit-devops-reviewer
    ├── audit-security-compliance
    └── audit-documentador    (al final)
```

## Contrato entre agentes
- Se comunican **solo por archivos** dentro de `qa-runs/<STORY_ID>/` (`RUN_DIR`).
- Cada agente devuelve a su orquestador un **estado corto**, nunca el contenido completo.
- Estructura de `RUN_DIR`:
```
00-historia.md
01-analisis/      requerimientos.md · preguntas-abiertas.md · casos-de-prueba.md
02-automatizacion/ archivos-generados.md · ejecucion-<n>.md · reporte.md
03-auditoria/     code-review.md · devops-review.md · seguridad.md · documentacion.md · hallazgos.md
RESUMEN.md
```

## Idioma
- Comunicación y reportes: español.
- Código: nombres en inglés, comentarios en español.

## Valores por defecto (si no existe qa.config.md)
- Backend: Java 17 + Spring Boot 3 → JUnit 5 + Spring Boot Test + RestAssured/MockMvc, `mvn test`
- Frontend: React 18 + Vite → Vitest + Testing Library (unitario), Playwright (e2e)
- BD de pruebas: PostgreSQL vía Testcontainers

## Límites
- Ningún agente hace commit, push ni merge.
- Ningún agente modifica código de producción.
- Ningún agente cambia el resultado esperado de un caso para que una prueba pase.
