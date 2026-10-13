# Presentación del proyecto ReflexIA

Guion listo para adaptar a diapositivas y exponer el proyecto completo. Preparado según la pauta **EVA1_Instrucciones_y_Pauta.docx** disponible para el equipo: presentación del alcance, demostración funcional y defensa oral en **15–20 minutos**. No reemplaza la ejecución en vivo desde la rama `main`.

> **Importante:** la solicitud mencionaba una pauta EVA2, pero el documento que se encontró y se confirmó usar es la pauta EVA1 adjunta. Si la pauta EVA2 tiene criterios distintos, este guion debe actualizarse.

## Ficha de exposición

- **Duración objetivo:** 18 minutos.
- **Audiencia y usuario principal:** estudiantes de pedagogía en práctica profesional; también profesor guía y administrador.
- **Problema abordado:** la reflexión sobre incidentes de aula y el seguimiento de los aprendizajes pueden quedar dispersos, ser difíciles de acompañar y exponer información sensible.
- **Propuesta:** acompañar un ciclo de reflexión pedagógica con actividades guiadas, resguardo de acceso por rol y seguimiento del avance, procurando que las orientaciones apoyen al estudiante sin escribir por él.
- **Participación:** repartir demostración y respuestas entre todos los integrantes.
- **Regla de honestidad:** explicar como prototipo cualquier flujo marcado como simulado o local. No presentar simulaciones, datos de ejemplo ni pendientes como servicios productivos.

## Orden y tiempos

| Momento | Tiempo | Contenido |
|---|---:|---|
| Presentación del alcance | 1:30 | Usuario, problema y recorrido de ReflexIA |
| Demostración funcional | 10:30 | Acceso, estudiante, docente, administrador y fuentes de datos |
| Preguntas del docente | 6:00 | React/TypeScript, Firebase, arquitectura, calidad y límites |
| **Total objetivo** | **18:00** | Dentro de los 15–20 minutos de la pauta |

## Diapositiva 1 — ReflexIA: acompañar la reflexión pedagógica (0:00–0:45)

**En pantalla**

- Plataforma web para la práctica profesional pedagógica.
- Reflexión guiada sobre incidentes críticos.
- Roles: estudiante, profesor guía y administrador.

**Relato sugerido**

> ReflexIA es una aplicación web para estudiantes de pedagogía en práctica profesional. Busca ordenar el análisis de incidentes de aula y facilitar el acompañamiento del profesor guía, con atención a la privacidad de las personas involucradas. La aplicación contempla tres perfiles: estudiante, profesor guía y administrador.

## Diapositiva 2 — Necesidad, propuesta y alcance (0:45–1:30)

**En pantalla**

- Necesidad: estructurar el ciclo reflexivo y el seguimiento.
- Propuesta: marco teórico, talleres guiados, revisión docente y avance.
- Alcance implementado: frontend React + TypeScript con Firebase en flujos concretos.

**Relato sugerido**

> El recorrido del estudiante parte con el marco teórico, continúa con talleres para analizar el incidente y registrar su reflexión, y se complementa con impulsos orientadores y una biblioteca de innovaciones. El docente puede revisar propuestas y seguir avances. La solución está implementada como frontend: algunas partes usan Firebase real y otras siguen siendo prototipos locales o simulaciones, que señalaremos durante la demostración.

## Demostración funcional — 10:30 (1:30–12:00)

### 1. Landing e inicio de sesión (1:30–2:35)

**Mostrar**

1. Landing pública y sus accesos.
2. Formulario de `/iniciar-sesion`.
3. Ingreso con una cuenta de prueba autorizada y redirección por rol.

**Explicar**

- El proyecto usa React Router para separar las rutas públicas y protegidas.
- Firebase Authentication comprueba identidad/credenciales; la whitelist en Firestore determina si el acceso está activo y qué rol tiene.
- La landing es contenido estático; no consulta Firebase.
- El acceso institucional es `@ucen.cl`; no se solicita RUT.

**Código que se puede señalar:** `src/App.tsx`, `src/views/auth/LoginView.tsx`, `src/context/AuthContext.tsx`, `src/services/authService.ts` y `src/services/whitelistService.ts`.

### 2. Recorrido de estudiante: inicio y evaluación diagnóstica (2:35–4:00)

**Mostrar**

1. Dashboard del estudiante y sus accesos.
2. Marco teórico en `/estudiante/marco-teorico`.
3. Estado de evaluación y bloqueo/desbloqueo de talleres.

**Explicar**

- El cuestionario utiliza un banco de preguntas, temporizador, intentos y resultado.
- El estado de aprobación se consulta desde el flujo de talleres para condicionar su acceso.
- La interfaz muestra el estado de carga, el resultado y el progreso.
- Aclarar que la corrección ocurre en el navegador en esta versión; no presentarla como verificación invulnerable o autoritativa de servidor.

**Código que se puede señalar:** `src/views/theory-verification/` y `src/views/critical-incidents/hooks/useTheoryGate.ts`.

### 3. Taller, borrador e impulso orientador (4:00–5:45)

**Mostrar**

1. Lista de talleres y apertura de un taller.
2. Pasos del asistente: contexto, descripción, actores e influencia, relevancia pedagógica.
3. Referencias teóricas, guardado de borrador e intentos restantes.
4. Solicitud del impulso, incluyendo su estado de carga.

**Explicar**

- El borrador se guarda en almacenamiento local particionado por UID; guardar no consume un intento.
- Pedir un impulso sí descuenta un intento.
- **El impulso actual es simulado localmente** mediante reglas y una espera simulada; no es una llamada a un modelo de IA. Entrega pistas generales y no redacta el texto del estudiante.
- Los intentos y relatos del taller no se envían a una base compartida en esta versión.

**Código que se puede señalar:** `src/views/critical-incidents/`, `src/services/criticalIncidentService.ts`, `src/utils/userStorage.ts` y `src/utils/impulseGenerator.ts`.

### 4. Detección de datos sensibles (5:45–6:30)

**Mostrar**

- Solo si el servicio está configurado: analizar un relato **sintético**, mostrar carga, resultado y corrección manual.

**Explicar con precisión**

- La detección usa OpenRouter desde el frontend y depende de la configuración de su API key.
- El texto de prueba se transmite al proveedor externo; no introducir nombres, colegios, cursos ni relatos reales durante la exposición.
- El detector destaca coincidencias para que la persona las corrija; no modifica el texto por ella.
- Una alerta no equivale a anonimización garantizada ni sustituye revisión humana. Si no hay configuración o red, explicar ese límite sin simular una respuesta exitosa.

**Código que se puede señalar:** `src/services/openRouterService.ts` y `src/views/critical-incidents/hooks/useSensitiveDataDetector.ts`.

### 5. Innovaciones pedagógicas (6:30–7:05)

**Mostrar**

- Biblioteca de `/estudiante/innovaciones` o `/docente/innovaciones`, búsqueda, filtros y detalle.

**Explicar**

- El catálogo mostrado está definido en datos locales de ejemplo; no es contenido consultado desde Firebase.

**Código que se puede señalar:** `src/views/innovations/`.

### 6. Vista docente: revisión y seguimiento (7:05–9:00)

**Mostrar**

1. `/docente/reflexiones`: propuesta original, editor y validación.
2. `/docente`: resumen, filtros y avance del estudiante.

**Explicar**

- Las reflexiones revisadas son ejemplos asignados a cuentas de prueba.
- La propuesta original se conserva; el docente puede editar y validar una nota.
- La nota oficial validada se guarda en Firestore (`evaluations`); los textos de revisión y las reflexiones de ejemplo no se distribuyen a la cuenta del estudiante.
- El panel docente cruza `whitelist`, `progress`, `profiles` y `evaluations`. `progress` contiene resúmenes de avance, no los relatos.
- Los nombres de `profiles` se cargan manualmente; el panel muestra estudiantes según los datos configurados.

**Código que se puede señalar:** `src/views/reflections/`, `src/services/reflectionService.ts`, `src/services/studentEvaluationService.ts` y `src/services/teacherDashboardService.ts`.

### 7. Administración y plazos (9:00–10:30)

**Mostrar**

1. `/admin/whitelist`: búsqueda/filtros y, si corresponde, alta, carga previa o revocación de una cuenta de prueba.
2. `/docente/plazos`: panel de fechas e intentos.

**Explicar**

- La whitelist sí opera sobre Cloud Firestore. No revocar ni alterar cuentas productivas durante la demo.
- El panel de plazos permite editar y guardar valores en `localStorage` del navegador del docente. **Aún no modifica los plazos ni intentos efectivos de los talleres**, que siguen usando valores fijos.
- El panel lo declara como datos simulados; describirlo como prototipo, no como configuración compartida.

**Código que se puede señalar:** `src/views/admin-whitelist/`, `src/services/whitelistService.ts` y `src/services/workPacingService.ts`.

### 8. Diseño adaptable y capas técnicas (10:30–12:00)

**Mostrar**

- Navegación por layouts y, si el tiempo lo permite, una vista a 360 px.
- En una vista técnica breve: árbol de rutas y separación de capas.

**Explicar**

- React 18 y TypeScript; Vite; React Router; Tailwind CSS.
- `App.tsx` define rutas anidadas y vistas con carga diferida (`lazy`/`Suspense`).
- Patrón por feature: modelos → servicios → hooks → componentes → vista.
- `AuthContext` comparte estado de sesión; hooks encapsulan lógica y estado de cada feature.
- Diseño mobile-first; verificar la experiencia real a 360 px y escritorio en vez de inferirla solo por las clases CSS.

**Código que se puede señalar:** `src/App.tsx`, `src/main.tsx`, `src/context/AuthContext.tsx` y una feature como `src/views/critical-incidents/`.

## Diapositiva de cierre — Qué demuestra y qué falta

**En pantalla**

- **Integraciones reales:** autenticación Firebase, autorización por whitelist y Firestore en whitelist, resumen `progress` y notas validadas.
- **Prototipos locales o contenido de ejemplo:** impulso formativo, reflexiones, biblioteca de innovaciones y configuración de plazos.
- **Siguiente paso de integración:** servicio real de IA/backend, persistencia compartida de relatos y reflexiones, y conexión de la configuración de plazos con los talleres.

**Relato sugerido**

> ReflexIA ya permite recorrer el flujo por roles y muestra integraciones concretas con Firebase, además de prototipos funcionales para el acompañamiento pedagógico. Para llevarlo a un uso institucional real, el paso principal es completar el backend compartido, conectar los datos de estudiantes y docentes y fortalecer la validación y privacidad del procesamiento de relatos.

## Defensa oral — preguntas probables y respuestas

### ¿Quién es el usuario y qué problema resuelve la aplicación?

Estudiantes de pedagogía en práctica profesional necesitan estructurar su reflexión sobre incidentes críticos; el profesor guía necesita revisar y acompañar su avance. ReflexIA organiza ese recorrido por etapas y roles.

### ¿Cómo se diferencia autenticación de autorización?

Firebase Authentication establece la identidad a partir de las credenciales. Firestore y el documento activo en `whitelist` determinan si esa identidad tiene acceso y qué rol le corresponde. Las reglas de Firestore son necesarias para proteger datos en servidor; una ruta protegida en React solo controla navegación.

### ¿Dónde están las rutas y cómo se restringen?

`src/App.tsx` declara rutas públicas y rutas anidadas bajo layouts. `RequireStudent` comprueba sesión y roles permitidos antes de representar los layouts protegidos.

### ¿Qué hooks de React se usan y por qué?

- `useState`: estado local de formularios y componentes.
- `useEffect`: suscripciones y sincronización con servicios/ciclo de vida.
- `useContext`: acceso al estado compartido de autenticación.
- Hooks personalizados: encapsulan lógica de cada feature para separar estado de presentación.

La respuesta debe acompañarse con ejemplos concretos del código abierto durante la defensa.

### ¿Cómo está estructurado el proyecto?

Por capas y features: los modelos definen contratos TypeScript, los servicios acceden a Firebase o almacenamiento, los hooks coordinan lógica y estado, y componentes/vistas muestran la interfaz.

### ¿Qué información es realmente compartida entre cuentas?

La whitelist y algunos datos de panel docente viven en Firestore, incluyendo resúmenes de progreso y notas validadas. Los borradores y relatos de talleres permanecen en `localStorage` particionado por UID; las reflexiones del panel docente son ejemplos. No afirmar que el sistema sincroniza relatos reales entre estudiantes y docentes.

### ¿El impulso y la detección sensible usan el mismo tipo de IA?

No. El impulso es una simulación local por reglas y no llama a una IA. El detector de datos sensibles utiliza OpenRouter desde el frontend, si hay configuración; es una integración externa distinta y debe demostrarse solo con texto sintético.

### ¿Los plazos que configura el docente cambian lo que ve el estudiante?

Todavía no. Se guardan en el almacenamiento local del navegador del docente; las actividades siguen usando valores fijos. Es una limitación conocida que debe conectarse a persistencia compartida y a los servicios de los talleres y cuestionario.

### ¿Cómo responderían ante un error de Firebase o de red?

La interfaz contempla estados de carga/error en los flujos relevantes; el acceso no debe concederse si no se puede autorizar. Durante la demo, señalar el mensaje observado y explicar el reintento; no fingir datos de éxito ni cambiar a una cuenta no autorizada.

## Preparación técnica para el día de la presentación

### Antes de salir

- Confirmar con el docente el repositorio y que la rama `main` es la que se debe ejecutar.
- Revisar accesibilidad del repositorio y evidencia de **al menos 10 commits incrementales propios por integrante**. No inferir autoría solo por el total de commits del grupo.
- Verificar cuentas de demostración activas en Firebase Authentication y con rol correcto en la whitelist.
- Preparar datos de prueba sintéticos para el flujo de incidentes y el detector de privacidad.
- Si se demostrará OpenRouter, revisar configuración local de `VITE_OPENROUTER_API_KEY` sin mostrar ni compartir el secreto. No registrar la clave en Git.
- Ensayar cada rol y el orden de las pantallas; limitar navegación no esencial para cumplir el tiempo.
- Probar la app en móvil (360 px) y escritorio; comprobar que todos los integrantes puedan explicar cualquier parte.

### En el computador de exposición

```bash
npm install
npm run lint
npm run build
npm run dev
```

Dejar el servidor iniciado antes de comenzar y usar solo `main`. No se requiere despliegue externo según la pauta; la demostración se ejecuta en vivo desde el repositorio.

### Criterios de la pauta EVA1 a evidenciar

| Criterio | Peso | Evidencia durante esta presentación |
|---|---:|---|
| Funcionalidad y alcance comprometido | 30% | Recorrer accesos y funciones implementadas; distinguir ejemplos y simulaciones |
| React y TypeScript | 20% | Rutas, props tipadas, estado, hooks, contexto y capas |
| Consumo de datos desde Firebase | 15% | Mostrar whitelist/autenticación y datos de Firestore efectivamente disponibles |
| Diseño visual y responsividad | 10% | Navegación y vistas a tamaños móvil/escritorio |
| Proceso de trabajo en GitHub | 15% | `main` funcional y commits incrementales por integrante |
| Defensa oral | 10% | Respuestas claras con referencias al código y decisiones reales |

## Referencias del repositorio

- [README del proyecto](../../README.md): requisitos, rutas y estado de implementación.
- [Guía de arquitectura de landing y login](./landingpage-login-arquitectura-de-software.md): secuencia de autenticación y preguntas de defensa.
- [Guía de HU-02](../historias-usuario/HU02_GUIA.md): límites de las simulaciones de impulso y revisión.
- [Guía del panel docente](../historias-usuario/PANEL_DOCENTE_GUIA.md): colecciones, sincronización y limitaciones actuales.
- [Guía de HU-05](../historias-usuario/HU05_GUIA.md): detector externo de datos sensibles.
- [Guía de HU-06](../historias-usuario/HU06_GUIA.md): persistencia local de la configuración de plazos.
