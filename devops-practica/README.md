# Práctica DevOps: Proceso y Automatización con GitHub Actions

## 1. El proceso de DevOps

DevOps es la práctica de unir desarrollo (Dev) y operaciones (Ops) en un ciclo
continuo, en lugar de tratarlos como equipos separados. El objetivo es
entregar software de forma más rápida, confiable y con menos fricción entre
"quien programa" y "quien despliega/mantiene".

El ciclo típico tiene estas fases:

1. **Plan** — Se definen requisitos, tareas e historias de usuario
   (herramientas como Jira, Trello).
2. **Code** — Se escribe el código, normalmente en un repositorio Git con
   ramas (feature branches, pull requests).
3. **Build** — El código se compila/empaqueta automáticamente.
4. **Test** — Se corren pruebas automáticas (unitarias, integración) para
   detectar errores antes de producción.
5. **Release** — El artefacto pasa las pruebas y queda listo para
   desplegarse.
6. **Deploy** — Se sube a un entorno (staging o producción), idealmente de
   forma automática.
7. **Operate** — La aplicación corre en producción; se monitorea su
   comportamiento.
8. **Monitor** — Se recogen métricas y logs para detectar problemas y
   retroalimentar el ciclo (vuelve a Plan).

### Pilares clave

- **CI (Integración Continua):** cada cambio de código se integra y prueba
  automáticamente con frecuencia.
- **CD (Entrega/Despliegue Continuo):** el software pasa de forma automática
  (o semi-automática) desde el código hasta producción.
- **Infraestructura como código (IaC):** la infraestructura se define en
  archivos versionables (Terraform, Ansible, etc.).
- **Automatización:** builds, pruebas y despliegues sin intervención manual
  repetitiva.
- **Colaboración y cultura:** desarrollo y operaciones comparten
  responsabilidad sobre todo el ciclo de vida del software.

## 2. Automatización con GitHub Actions

Este repositorio incluye un ejemplo funcional de **Integración Continua
(CI)** ubicado en `.github/workflows/ci.yml`.

### ¿Qué hace?

- Se activa automáticamente en cada `push` o `pull request` hacia la rama
  `main`.
- Instala las dependencias del proyecto (`npm ci`).
- Corre el linter, si el proyecto lo tiene configurado.
- Ejecuta las pruebas automatizadas (`npm test`).
- Construye el proyecto (`npm run build`), si aplica.
- Prueba el código en dos versiones de Node.js (18.x y 20.x) usando una
  matriz de ejecución.

### ¿Cómo usarlo en tu propio proyecto?

1. Copia la carpeta `.github/workflows/` a la raíz de tu repositorio.
2. Asegúrate de tener un `package.json` con scripts `test`, `lint` y/o
   `build` (los que no existan simplemente se omiten gracias a
   `--if-present`).
3. Haz `git push` a la rama `main` o abre un pull request.
4. Ve a la pestaña **Actions** en GitHub para ver el workflow ejecutarse.

### Por qué es un buen ejemplo de DevOps en miniatura

- Automatiza los pasos de **Build** y **Test** del ciclo: no hay que correr
  los comandos a mano cada vez.
- Se dispara solo con eventos de Git (push/PR), que es la esencia de CI.
- Es fácilmente extensible: se le puede agregar un paso de **despliegue**
  (CD) para completar el ciclo hasta producción.
