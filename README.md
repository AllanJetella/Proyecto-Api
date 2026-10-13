# Remediación de Vulnerabilidades y Análisis de Seguridad OWASP ZAP

**Proyecto:** WebEmpresa (.NET Blazor) & ApiEmpresa (Web API .NET / MySQL)  
**Herramienta de Análisis:** OWASP ZAP v2.17.0  

---

## 📋 Resumen de la Entrega

Este repositorio contiene la remediación de vulnerabilidades detectadas en la aplicación web mediante la implementación de un middleware de seguridad en .NET para la configuración de cabeceras HTTP de protección y políticas de seguridad de contenido (CSP).

---

## 📊 Tabla Comparativa de Resultados (Antes vs. Después)

| Alerta Encontrada | Riesgo | Estado Inicial | Corrección Aplicada | Estado Final |
| :--- | :--- | :--- | :--- | :--- |
| **Falta encabezado X-Content-Type-Options** | Bajo | Detectado | Se inyectó el encabezado `X-Content-Type-Options: nosniff` en el middleware de .NET (`Program.cs`) para prevenir ataques de MIME-Sniffing. | **Corregida** |
| **CSP: Directivas sin Fallback** | Medio | Detectado | Se definieron explícitamente las directivas `form-action 'self'` y `frame-ancestors 'self'` en la cabecera `Content-Security-Policy`. | **Corregida** |
| **CSP: Directiva Wildcard** | Medio | Detectado | Se eliminaron fuentes abiertas comodín y se acotaron los orígenes permitidos (`'self'`, `ws:`, `wss:`, `http://localhost:5264`). | **Corregida** |
| **CSP: script-src unsafe-inline / eval** | Medio | Detectado | Se definieron en la directiva CSP. Requeridas funcionalmente por el motor de renderizado y circuitos SignalR de Blazor (`blazor.web.js`). | **Mitigada** |
| **CSP: style-src unsafe-inline** | Medio | Detectado | Se definieron en la directiva CSP. Requeridas por el aislamiento de estilos CSS de Blazor y Bootstrap. | **Mitigada** |
| **Aplicación Web Moderna** | Informativo | Detectado | Diagnóstico de ZAP al detectar manipulación dinámica del DOM (SPA / Blazor). | **Informativa** |
| **Comentarios Sospechosos** | Informativo | Detectado | Código generado automáticamente por el compilador de Blazor/Razor. No expone credenciales ni datos sensibles. | **Falso Positivo** |
| **Gestión de Sesión Identificada** | Informativo | Detectado | Cookie Antiforgery `.AspNetCore.Antiforgery.*` configurada con atributos `SameSite=Strict` y `HttpOnly`. | **Documentada** |

---

## 📁 Archivos de Evidencia

- 📄 **`Informe_ZAP_Antes.html`**: Informe completo de OWASP ZAP generado previo a la implementación de las medidas de seguridad.
- 📄 **`Informe_ZAP_Despues.html`**: Informe generado tras la incorporación del middleware de cabeceras de seguridad en `WebEmpresa/Program.cs`.