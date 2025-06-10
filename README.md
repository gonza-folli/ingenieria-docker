# **Proyecto Web Dockerizado: `Ingenieria-Docker`**

Este repo contiene el código de una sencilla página web estática (HTML y CSS) y ha sido dockerizado utilizando la imágen de **Nginx**. El proceso para construir y ejecutar el contenedor Docker es el siguiente.

---

## **📋 Pre - Requisitos**
- Docker instalado.
- Git.

---

## **🚀 Proceso para levantar el proyecto**

### **1. Clonar el repositorio**
Para clonar el repositorio se debe ejecutar el siguiente comando en alguna consola como git Bash.
```bash
git clone https://github.com/gonza-folli/ingenieria-docker.git
cd ingenieria-docker
```
Debería ver la siguiente **estructura**
```
ingenieria-docker/
├── css/
│   └── styles.css      # Archivos CSS
├── index.html          # Página principal
└── Dockerfile          # Configuración de Docker
```

## **🐳 Explicación del Dockerfile**
El archivo `Dockerfile` contiene las siguientes instrucciones:

```dockerfile
FROM nginx:alpine

COPY . /usr/share/nginx/html
```

### **¿Qué hace cada línea?**
1. **`FROM nginx:alpine`**  
   - Utiliza la imagen oficial de Nginx basada en Alpine Linux.
   - Esta imagen ya incluye un servidor web Nginx configurado para servir archivos estáticos.

2. **`COPY . /usr/share/nginx/html`**  
   - Copia **todos los archivos locales** (HTML, CSS, etc.) al directorio `/usr/share/nginx/html` dentro del contenedor.
   - Este es el directorio predeterminado donde Nginx busca los archivos para servir.

---

### **2. Construir la imagen Docker**
Desde la raíz del proyecto, ejecuta:
```bash
docker build -t trabajo-ingenieria .
```
Lo que hace este comando es ponerle nombre a la imágen, en este caso se llamará trabajo-ingenieria. A su vez el punto final indica que el Dockerfile esta en el directorio actual (por eso en el paso anterior ejecutamos cd ingenieria-docker)


### **3. Ejecutar el contenedor**
```bash
docker run -d -p 8080:80 --name web-dockerizada trabajo-ingenieria
```

El -p se ocupa de apuntar el puerto 80 del contenedor al 8080 de la PC. Se puede cambiar el 8080 por el puerto que se desee.

### **4. Acceder a la aplicación**
Ingresar a la siguiente URL donde 8080 es el puerto asignado
🔗 **[http://localhost:8080](http://localhost:8080)**  

Si todo funcionó correctamente, verá la página web levantada. En caso que en el paso anterior se haya modificado el puerto 8080, se deberá cambiarlo también en esta URL.

### **5. Detener el contenedor donde corre la aplicación**
```bash
docker stop web-dockerizada
```

---

## **📌 Notas**
- Si cambias los archivos locales, se debe volver a ejecutar desde el paso 2 para ver los cambios impactados
   ```bash
   docker stop web-dockerizada
   docker rm web-dockerizada
   docker run -d -p 8080:80 --name web-dockerizada trabajo-ingenieria
   ```
 - La imagen elegida `nginx:alpine` es ligera, ideal para proyectos simples.

---