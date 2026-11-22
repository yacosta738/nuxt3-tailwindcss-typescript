# Tarea RPI: corregir build de Nuxt/Vue

## Ruta
Delegated direct. Reproducir primero el fallo y aplicar la corrección mínima confirmada por evidencia.

## Tareas
- [x] RPI-001 Instalar dependencias y reproducir `npm run build`: falla en `nuxt-welcome.vue:9` con `Unexpected token`.
- [x] RPI-002 Confirmar el desajuste: rango prerelease flexible y sin lockfile, que permitía Vue 3.5.46 frente a las versiones 3.2.20 requeridas por el builder Nuxt; además, Vue Router 4.6.5 no coincide con el módulo CommonJS esperado por este Nuxt antiguo.
- [x] RPI-003 Fijar Nuxt 3.0.0-27243097.0b634e1, Vue 3.2.20 y Vue Router 4.0.12; agregar lockfile de npm.
- [x] RPI-004 Validar con `npm ci`, `npm ls nuxt3 vue @vue/compiler-sfc @nuxt/vite-builder vite vue-router --depth=2`, `npm run build` y `git diff --check`.
- [ ] RPI-005 Crear una PR dirigida a `main` y registrar el enlace.

## Criterios de aceptación
- El error de parseo del componente Vue se reproduce antes del arreglo.
- `npm run build` pasa después del arreglo.
- La PR contiene solo cambios necesarios y evidencia de validación.

## Evidencia
- Antes del cambio, `npm run build` falló de forma reproducible al parsear `node_modules/nuxt3/dist/app/components/nuxt-welcome.vue`.
- Con Vue 3.2.20 pero Vue Router 4.6.5, el build pasó el cliente y falló al resolver un archivo CommonJS antiguo de Vue Router.
- Con el conjunto fijado y lockfile, `npm ci` y `npm run build` pasaron; `git diff --check` también pasó.
- Instalación reporta 37 vulnerabilidades de dependencias antiguas. No se corrigieron en esta PR.

## Estado
Checking — la corrección y validación local terminaron; preparando la PR.

## Próximo paso
Revisar diff, commit, push y abrir la PR contra `main`.
