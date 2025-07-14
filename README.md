# 🎹 Toquen el DOM

<img src="assets/img/logo-blanca.png" alt="LetItBeat!" />

## /// 1. Descripción del Proyecto

Toquen el DOM es una aplicación web interactiva para una **escuela de música online** que permite a los usuarios practicar con **instrumentos virtuales** (Piano, Marimba y Batería) mediante interacción con teclado y mouse.

Este proyecto fue desarrollado como parte del **Bootcamp P1 de FemCoders**. (Proyecto ficticio de uso educacional)

## /// 2. Características Principales

- **Tres instrumentos** con sonidos realistas.
- Interacción dual **(teclado físico + mouse)**.
- **Animaciones** visuales al tocar.
- Diseño **responsive** con media queries.
- Fácil despliegue en local con **Docker**.

## /// 3. Contexto y Objetivos

**Aplicar y consolidar** conocimientos en JavaScript, HTML, CSS y Docker para crear una herramienta innovadora que facilite el aprendizaje musical en línea, sin importar la ubicación del estudiante.

- ➡️ Crear una plataforma interactiva para práctica musical.
- ➡️ Implementar interacción mediante mouse y teclado.
- ➡️ Implementar diseño adaptable (responsive).
- ➡️ Practicar contenedorización con Docker.

## /// 4. Requerimientos Técnicos

- ✅ **GitFlow** para gestión de versiones.
- ✅ Tres instrumentos: **Piano, Marimba y Batería**.
- ✅ Interacción con **mouse y teclado**.
- ✅ **Sonidos realistas** y sincronizados.
- ✅ **Animaciones** al tocar.
- ✅ Código **limpio y semántico** (HTML5, CSS3, JS Vanilla).
- ✅ **Responsive** (media queries).
- ✅ **Dockerfile** para contenedorización y despliegue local.

**Bonus track 🌟**

- Documentación clara y detallada.
- Preparado para futuros despliegues en servidor.

## /// 5. Vistas Principales

### Piano 🎹

- 2 octavas **completas**.
- Teclas blancas/negras correctamente **afinadas**.
- Mapeo a **teclado QWERTY**.

### Marimba 🎵

- Barras **organizadas** por tonalidad.
- Sonidos percusivos **realistas**.
- Visualización de **notas activas**.

### Batería 🥁

- Componentes **interactivos**.
- Efectos **visuales** al tocar.

## /// 6. Herramientas Utilizadas

- HTML5 semántico
- CSS3 (con media queries)
- JavaScript vanilla
- Docker y NGINX (para despliegue local)
- Git y GitHub
- DevTools
- Tone.js
- Google Fonts y Font Awesome
- Canva

## /// 7. Instalación y Uso

### ✅ Clonar el repositorio

```bash
git clone https://github.com/Alexandracoder/toqueneldom.git
cd toqueneldom
```

### ✅ Ejecutar en local con Docker

**Construir la imagen Docker:**

```bash
docker build -t toqueneldom-web .
```

**Ejecutar el contenedor:**

```bash
docker run -d -p 8080:80 --name toqueneldom-container toqueneldom-web
```

**Abrir en tu navegador:**

```
http://localhost:8080
```

### ⚡ Justificación del uso de Docker

Aunque es un proyecto frontend estático, Docker se usa para garantizar que todos puedan verlo exactamente igual, practicar la contenedorización y simular un posible despliegue real en un servidor NGINX.

## /// 8. Hecho por

- Murry Alexandra Rojas Castro
- Bruna H. Sonda Santos
- Débora Rubio
- Mayleth Carrascal

📅 Fecha de entrega: 24/04

🌐 **Repositorio:** [GitHub]https://github.com/Alexandracoder/toqueneldom.git)

Gracias! ✨
