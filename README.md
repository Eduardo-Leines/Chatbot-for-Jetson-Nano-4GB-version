# Chatbot para Laboratorio Alan Turing (EPN) para Jetson Nano 4GB

Este proyecto implementa un sistema de preguntas y respuestas (QA) utilizando un modelo de lenguaje grande (LLM) bajo la arquitectura de **Generación Aumentada por Recuperación (RAG)**. Su propósito es servir como un asistente virtual capaz de responder consultas específicas y contextualizadas sobre el **Laboratorio de Investigación en Inteligencia y Visión Artificial “Alan Turing”** de la Escuela Politécnica Nacional (EPN), basándose exclusivamente en una base de conocimiento interna.

## Funcionalidad del Proyecto

* **Arquitectura RAG:** El sistema recupera información relevante de una base de datos vectorial antes de generar una respuesta. Este enfoque garantiza que la información proporcionada por el LLM sea precisa y verificable contra los documentos fuente del Laboratorio.
* **Base de Conocimiento Específica:** Utiliza fragmentos de texto (chunks) que detallan información fundamental del Laboratorio, incluyendo datos de contacto, miembros del equipo, proyectos, publicaciones e historial.
* **Vectorización y Búsqueda Semántica:** Los fragmentos de conocimiento se convierten en *embeddings* utilizando un modelo especializado y se indexan con **FAISS** para una recuperación eficiente del contexto que mejor se ajusta a la pregunta del usuario.
* **Adaptabilidad de Modelos:** El diseño permite cargar modelos de lenguaje (LLMs) y de *embeddings* desde el *Hugging Face Hub* o desde una ubicación local. Esto es crucial para la implementación en entornos con recursos limitados o con restricciones de red (e.g., configuraciones en dispositivos como Jetson Nano).

## Tecnologías y Modelos

| Componente | Modelo/Biblioteca Principal | Propósito |
| :--- | :--- | :--- |
| **LLM (Generación)** | `google/flan-t5-small` | Modela la respuesta final en idioma español. Se utiliza la versión "small" por su eficiencia. |
| **Embedding (Codificación)** | `intfloat/multilingual-e5-small` | Crea las representaciones vectoriales del texto para la búsqueda semántica. |
| **Indexado Vectorial** | `faiss-cpu` | Biblioteca para el almacenamiento y la consulta rápida de los vectores. |
| **Plataforma** | `Jupyter Notebook`, `PyTorch`, `Transformers` | Entorno de desarrollo e infraestructura de modelos de lenguaje. |

## Guía de Instalación y Configuración

### Requisitos

* Python 3.x
* Un entorno de desarrollo compatible con Jupyter (JupyterLab o Google Colab).

### Pasos de Instalación

1.  **Instalar Dependencias:** Ejecute el siguiente comando para asegurar que todas las librerías requeridas estén instaladas.

    ```bash
    !pip3 install --upgrade pip setuptools wheel
    !pip3 install -q torch torchvision transformers ipywidgets beautifulsoup4 sentence_transformers faiss-cpu
    ```

2.  **Configuración de Entorno (Opcional):** En sistemas Linux con arquitecturas específicas (como Jetson Nano), puede ser necesario pre-cargar la librería Gomp:

    ```bash
    %env LD_PRELOAD=/usr/lib/aarch64-linux-gnu/libgomp.so.1
    ```

3.  **Carga de Modelos:** Verifique que los modelos `google/flan-t5-small` e `intfloat/multilingual-e5-small` sean accesibles por el *notebook*, ya sea a través de la descarga automática o desde una carpeta local.

## Uso

1.  Abra y ejecute el `Chatbot.ipynb` en un entorno Jupyter.
2.  Ejecute todas las celdas en orden.
3.  Una vez desplegada la interfaz de chat interactiva, formule preguntas relacionadas con la investigación, el equipo, o la logística del Laboratorio Alan Turing.

### Temas cubiertos por la base de conocimiento:

* Información sobre el equipo de investigación (directores, investigadores principales y colaboradores).
* Proyectos de investigación actuales, especialmente aquellos en **Reconocimiento de Gestos de la Mano (HGR)** y control de robots.
* Publicaciones científicas relevantes y métricas de producción académica.
* Datos de contacto y ubicación física.
* Procedimientos para pasantías o trabajos de tesis.

## Contacto y Colaboración

Para consultas sobre el Laboratorio, oportunidades de pasantías, o propuestas de tesis, por favor contacte al equipo de investigación a través del correo electrónico oficial: `laboratorio.ia@epn.edu.ec`.