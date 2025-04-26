# Despliegue de la Aplicación Pokédex en Azure

Este documento detalla el proceso paso a paso para desplegar la aplicación Pokédex en la nube utilizando la plataforma Azure.

---

## 1. Preparación del Proyecto

- Se descargó el repositorio base desde GitHub:  
  [https://github.com/rcuello/ac4dem1a](https://github.com/rcuello/ac4dem1a)

- Se extrajo el código dentro de la carpeta:  
  `sistemas-distribuidos/poke-dex-lab/source/pokedex-angular`

---

## 2. Prueba local

- Se accedió a la carpeta del proyecto:
  ```bash
  cd ruta/del/proyecto/pokedex-angular

- Se instalaron las dependencias necesarias.

- Se ejecutó localmente el proyecto.

- Se verificó el correcto funcionamiento accediendo a:
👉 http://localhost:4200

---

## 3. Subida del proyecto a GitHub

- Se creó un nuevo repositorio en GitHub con el nombre pokedex.

- Se subió el contenido del proyecto Angular (pokedex-angular) a dicho repositorio.

---

## 4. Creación de cuenta en Azure

- Se accedió a la página oficial: https://Azure.com

- Se creó una cuenta utilizando el inicio de sesión con GitHub.

- Se autorizó a Azure para acceder a los repositorios.

- Se eligió el plan gratuito Hobby.

---

## 5. Despliegue en Azure

- En el panel de Azure se seleccionó la opción "Add New Project".

- Se seleccionó el repositorio pokedex importado desde GitHub.

- Azure detectó automáticamente el framework Angular.

- No se modificaron las configuraciones por defecto.

- Se hizo clic en el botón Deploy.

---

## 6. Eventualidad en el Despliegue

Una vez completado el despliegue en Azure, se probó la aplicación en el dominio generado por la plataforma. Sin embargo, se detectó que las **imágenes no se mostraban correctamente.**

🔍 **Diagnóstico:**

El problema estaba relacionado con la ruta configurada para acceder a las imágenes dentro del proyecto. En el archivo `src/environments/environment.prod.ts` la propiedad `imagesPath` estaba definida como:

```ts
imagesPath: '/pokedex-angular/assets/images'
```

- Esta ruta no era válida en el entorno de producción, ya que el contenido estaba sirviéndose desde la raíz del dominio.

✅ **Solución:**

Se modificó la propiedad para utilizar la ruta correcta:

```ts
imagesPath: '/assets/images'
```

### 6.1 Aumentar la seguridad de la aplicación

Para mejorar la seguridad de mi Pokedex, añadí un archivo llamado **staticwebapp.config.json** en el directorio de despliegue. Su contenido fue el siguiente:

```json
{
  "globalHeaders": {
    "Content-Security-Policy": "default-src * 'unsafe-inline' 'unsafe-eval' data: blob:;",
    "X-Frame-Options": "ALLOWALL",
    "Permissions-Policy": "geolocation=*, camera=*, microphone=*"
  }
}
```

---

✅ **Estado final**

- La aplicación fue desplegada correctamente en Vercel.

- Todos los recursos se cargan sin inconvenientes.

- El dominio proporcionado por Vercel muestra la Pokédex con funcionalidad completa.



