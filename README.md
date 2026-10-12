# Práctica: GitHub Actions + Surge.sh

**Autor:** Danny Peña Adames  
**Matrícula:** 2025-1124  
**Objetivo:** publicar automáticamente una página HTML en Surge.sh al hacer `git push` a la rama `main`.

## Estructura

- `index.html`: página principal, con estilos CSS integrados.
- `.github/workflows/main.yaml`: automatización de GitHub Actions.
- `.gitignore`: ignora el directorio temporal `dist/`.

## Configuración inicial

1. Instala Git y Node.js 18 o superior (preferible Node 22 LTS).
2. Crea un repositorio **público, vacío, sin README** llamado `practica-github-actions-surge` en tu cuenta de GitHub (`dannypena1026`).
3. Extrae este ZIP y abre **Git Bash** dentro de la carpeta `practica-github-actions-surge`.
4. Ejecuta:

   ```bash
   git init -b main
   git add .
   git commit -m "Agregar pagina web e integracion continua"
   git remote add origin https://github.com/dannypena1026/practica-github-actions-surge.git
   ```

   Todavía **no** hagas `push`: primero debes guardar el secreto.

5. Instala Surge y entra a tu cuenta desde Git Bash:

   ```bash
   npm install --global surge
   surge login
   ```

6. Genera un token exclusivo para el dominio del proyecto:

   ```bash
   surge tokens add --domain dannypena1026-2025-1124-ci.surge.sh -m "github-actions-itla"
   ```

   Copia el token que aparece. **No lo compartas, no lo pegues en el repositorio ni lo guardes en ningún archivo versionado.**

7. En el repositorio de GitHub, entra a **Settings > Secrets and variables > Actions > New repository secret**. Ponle exactamente `SURGE_TOKEN` y pega el token que generaste.

8. Ahora sí, en Git Bash ejecuta:

   ```bash
   git push -u origin main
   ```

9. Abre la pestaña **Actions** del repositorio. El workflow `Despliegue continuo a Surge.sh` debe aparecer. Cuando finalice correctamente, visita:

   `https://dannypena1026-2025-1124-ci.surge.sh`

   **Importante:** este subdominio es una propuesta, no se ha confirmado que esté disponible. Si ya está ocupado, cambia el dominio tanto en el YAML como en el comando `surge tokens add` antes de guardar el token.

## Prueba de despliegue automático

Modifica una palabra de `index.html`, guarda y ejecuta:

```bash
git add index.html
git commit -m "Probar despliegue automatico"
git push
```

Comprueba que el nuevo flujo aparece en Actions, termina correctamente y la página refleja el cambio.

## Enlace para entregar

`https://github.com/dannypena1026/practica-github-actions-surge`

> El repositorio y la web solo existirán después de crearlos/publicarlos. Este ZIP contiene los archivos listos, pero no configura tu cuenta de Surge ni crea el secreto por sí solo.
