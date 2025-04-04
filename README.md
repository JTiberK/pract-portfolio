# **Portafolio Estático con Amazon S3 y CloudFront**

<p align="Center">

<img src="/images/portfolio1.jpg" width="300px">
   
</p>

Este repositorio contiene el código fuente de un sitio web estático diseñado para ser desplegado en **Amazon S3** y distribuido mediante **Amazon CloudFront**. A continuación, se describe resumidamente el propósito del proyecto y cómo funciona CloudFront.

---

## **Descripción del Proyecto**

Este proyecto consiste en un **portafolio personal** alojado en un bucket de Amazon S3. Además, utiliza **Amazon CloudFront** como red de entrega de contenido (CDN) para mejorar la velocidad, seguridad y disponibilidad del sitio web.

El sitio también incluye una sección de ecommerce (`/shop`) que se aloja en un segundo bucket de S3. CloudFront actúa como un "multiplexor" que enruta las solicitudes a los buckets correctos según la ruta solicitada.

---

## **¿Qué es Amazon CloudFront?**

**Amazon CloudFront** es un servicio de red de entrega de contenido (CDN) que acelera la entrega de tus aplicaciones web o sitios estáticos a usuarios globales. Funciona almacenando copias de tu contenido en puntos de presencia (PoP) distribuidos globalmente, lo que reduce la latencia y mejora la experiencia del usuario.

### **Beneficios de CloudFront en este Proyecto**
1. **Velocidad Mejorada:**
   - CloudFront entrega el contenido desde el PoP más cercano al usuario, reduciendo la latencia.
   
2. **Distribución Basada en Rutas:**
   - La ruta raíz (`/`) apunta al bucket del portafolio.
   - La ruta `/shop/*` apunta al bucket del ecommerce.

3. **Caché de Contenido:**
   - CloudFront almacena en caché las respuestas de los buckets S3, lo que reduce la carga en los buckets y mejora el rendimiento.

4. **Seguridad Mejorada:**
   - Soporte para HTTPS asegura que el tráfico entre los usuarios y tu sitio sea cifrado.
   - Protección contra ataques DDoS gracias a AWS Shield Standard.

5. **Optimización de Costos:**
   - Al reducir el número de solicitudes directas a los buckets S3, CloudFront puede ayudar a ahorrar en costos de almacenamiento y transferencia de datos.

---

## **Estructura del Proyecto**

El proyecto está organizado de la siguiente manera:

```
mi-portafolio/
├── index.html          # Página principal del portafolio
├── images/             # Imágenes utilizadas en el sitio
├── style/              # Archivos CSS para estilos
└── README.md           # Este archivo
```

---

## **Cómo Funciona CloudFront en este Proyecto**

1. **Origen Principal:**
   - El bucket `nombre-bucket-2` contiene el contenido del portafolio y actúa como origen principal de CloudFront.

2. **Segundo Origen:**
   - El bucket `nombre-bucket-1` contiene la carpeta `/shop` con el contenido del ecommerce.

3. **Comportamientos (Behaviors):**
   - **Ruta Raíz (`/`):** Entrega contenido desde `nombre-bucket-2` (portafolio).
   - **Ruta `/shop/*`:** Entrega contenido desde `nombre-bucket-1` (ecommerce).

4. **Entrega Global:**
   - Los usuarios acceden al sitio a través de la URL de CloudFront, por ejemplo:
     - Portafolio: `https://tu-distribucion.cloudfront.net`
     - Ecommerce: `https://tu-distribucion.cloudfront.net/shop/`

---

## **Instrucciones para Desplegar el Sitio**

1. **Clonar el Repositorio:**
   ```bash
   git clone https://github.com/tu-usuario/my-portfolio.git
   cd my-portfolio/
   ```

2. **Subir los Archivos a S3:**
   - Para el portafolio:
     ```bash
     aws s3 cp . s3://nombre-bucket-2/ --recursive
     ```
   - Para el ecommerce:
     ```bash
     aws s3 cp shop/ s3://nombre-bucket-1/shop/ --recursive
     ```

3. **Configurar CloudFront:**
   - Crea una distribución en CloudFront con los siguientes orígenes:
     - Origen 1: `nombre-bucket-2` (portafolio).
     - Origen 2: `nombre-bucket-1` (ecommerce).
   - Configura los comportamientos basados en rutas.

4. **Probar el Sitio:**
   - Accede a las URLs de CloudFront para verificar que todo funcione correctamente.

---

## **Recursos Adicionales**

- [Documentación de Amazon S3](https://docs.aws.amazon.com/s3/)
- [Documentación de Amazon CloudFront](https://docs.aws.amazon.com/cloudfront/)
- [Guía de GitHub Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

---

## **Contribuciones**

Si deseas contribuir a este proyecto, siéntete libre de abrir un issue o enviar un pull request. ¡Toda ayuda es bienvenida!

---

## **Licencia**

Este proyecto está bajo la licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más detalles.
