---
title: "Información general y arquitectura | Documentos de Microsoft"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7549b59d4edc00dd620deeb515f6cd7143a62db7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---

# <a name="architecture-and-overview-of-machine-learning-services"></a>Información general de servicios de aprendizaje de máquina y arquitectura

En este tema se describe los objetivos de la biblioteca extensibility framework que admite la ejecución del script de Python y R en SQL Server.

También proporciona una visión general de cómo la arquitectura está diseñada para cumplir estos objetivos, cómo se admiten y ejecuta SQL Server y las ventajas de la integración de R y Python.

En general, el marco de extensibilidad es casi idéntico para R y Python, con algunas diferencias menores en los detalles de los iniciadores que se llaman, opciones de configuración y así sucesivamente. Para obtener más información acerca de la implementación para un idioma específico, vea estos temas:

- [Introducción a la arquitectura de SQL Server R Services](r/architecture-overview-sql-server-r.md)
- [Introducción a la arquitectura de Python en SQL Server](python/architecture-overview-sql-server-python.md)


## <a name="background"></a>Información previa

En SQL Server 2016, se introdujeron numerosos cambios en el motor de base de datos para admitir la ejecución de scripts de R mediante SQL Server. En SQL Server de 2017 esta infraestructura subyacente se ha mejorado para agregar compatibilidad para el lenguaje de Python.

El objetivo del marco de extensibilidad era crear una interfaz entre SQL Server y lenguajes de ciencia de datos, como R y Python, para reducir la fricción que tiene lugar cuando se muevan las soluciones de ciencia de datos en producción y para proteger los datos que podrían ser mejor muestre durante el proceso de desarrollo de ciencia de datos.

Mediante la ejecución de un lenguaje de scripting de confianza dentro de un entorno seguro administrado por SQL Server, el desarrollador de la base de datos puede mantener la seguridad al tiempo que permite a los científicos de datos utilizar datos de la empresa.

  ![Objetivos de la integración con SQL Server](media/ml-service-value-add.png "servicios de valor agregado de aprendizaje de máquina")

- Los usuarios actuales de R o Python deben ser capaz de trasladar su código y ejecutarlo en SQL Server con relativamente pequeñas modificaciones.
- El modelo de seguridad de datos en SQL Server se extiende a los datos utilizados por los lenguajes de script externo. En otras palabras, un usuario ejecuta el script de R o Python no podrá utilizar los datos que podrían no tener acceso a ese usuario en una consulta SQL.
- El Administrador de base de datos debe ser capaz de administrar los recursos utilizados por scripts externos, administrar usuarios y administrar y supervisar las bibliotecas de código externo.
- El sistema debe admitir soluciones que se basa completamente en distribuciones de código abierto de R y Python, pero use propietarios componentes desarrollados por Microsoft para proporcionar mayor seguridad y rendimiento.

## <a name="architecture-core-concepts"></a>Conceptos básicos de arquitectura

Para cumplir estos objetivos, la arquitectura de SQL Server 2016 R Services y servicios de aprendizaje de SQL Server de 2017 máquina para R y Python se basa en estos conceptos básicos:

+ **Arquitectura de varios proceso**

  R y Python es lenguajes de código abierto con compatibilidad enriquecida y entusiasta comunidad. Por lo tanto, es importante mantener una interoperabilidad completa con R de código abierto y Python.

  Distribuciones de código abierto de R y Python se instalan con SQL Server bajo licencia y pueden funcionar de forma independiente de SQL Server si es necesario.

   Además, Microsoft proporciona un conjunto de bibliotecas de propietarios que proporcionan integración con SQL Server, incluida la traducción de datos, compresión y optimización destinados a cada idioma admitido.

+ **Seguridad**

   Mejorar la seguridad significa soporte para la autenticación de Windows integrada y basada en contraseña inicios de sesión SQL, como control también lo más segura de credenciales, dependencia de SQL Server para la protección de datos y el uso de SQL Server de confianza Launchpad para administrar scripts externos ejecución y proteger los datos utilizados en las secuencias de comandos.

+ **Escalabilidad y rendimiento**

  Integración con SQL Server es clave para la mejora de la utilidad de R y Python en la empresa. Se puede ejecutar cualquier secuencia de comandos de R o Python mediante una llamada a un procedimiento almacenado, y los resultados se devuelven como resultados tabulares directamente a SQL Server, lo que facilita generar o consumir aprendizaje automático desde cualquier aplicación que pueda enviar una consulta SQL y controlar los resultados.

  Optimización del rendimiento se basa en dos aspectos igualmente eficaces de la plataforma: la regulación de recursos y paralelo procesamiento con SQL Server e informática proporcionada por los algoritmos de **RevoScaleR** y **revoscalepy**.


## <a name="solution-development-and-deployment"></a>Implementación y desarrollo de soluciones

Además de estos objetivos de núcleo para la plataforma de extensibilidad, los servicios de aprendizaje de máquina en SQL Server están diseñados para proporcionar una integración segura con el motor de base de datos y la pila de BI, con estas ventajas:

+ Administración del rendimiento y recursos a través de las herramientas tradicionales de supervisión
+ Usar la forma más fácil de Python y R datos mediante conjuntos de BI o cualquier aplicación que se puede utilizar los resultados de la consulta SQL
+ Cantidad inferior barrera para el desarrollo empresarial de soluciones de aprendizaje de máquina

Vamos a ver cómo funciona en la práctica.

  ![Proceso de desarrollo de soluciones de aprendizaje automático](media/ml-solution-development-process.png "desarrollar e implementar con servicios de aprendizaje de máquina")

1. Datos se conservan dentro del límite de cumplimiento de normas y uso de datos puede administrarse y supervisado por SQL Server. Mientras tanto, el DBA tiene control total sobre quién puede instalar paquetes o ejecutar secuencias de comandos en el servidor. Si lo desea, el DBA puede delegar permisos en el nivel de base de datos a los científicos de datos o a administradores.
2. Los científicos de datos pueden crear y probar soluciones en sus entornos preferidos de R o Python, desconectados del servidor.
3. El programador SQL puede utilizar herramientas conocidas como Management Studio o Visual Studio para integrar el código de R o Python con SQL Server. La estrecha integración significa que el desarrollador experto puede elegir la mejor herramienta para optimizar cada tarea. Por ejemplo, podría usar SQL para algunas tareas de ingeniería de característica y R para que otros usuarios. Puede incrustar el script de Python en una tarea de Integration Services para realizar análisis de texto sofisticadas.
4. Probado y listo para implementar las soluciones se pueden optimizar mediante tecnologías de SQL Server, como índices de almacén de columnas, para mejorar el rendimiento. Nuevas características le permiten lote-entrenar varios modelos pequeños en paralelo en el conjunto de datos con particiones o puntuación millones de filas en que se usa código nativo de SQL optimizado para tareas de aprendizaje automático.
5. ¿Listo para elevación? Puede exponer fácilmente sus soluciones de predicción en la pila de BI o las aplicaciones externas mediante procedimientos almacenados.

## <a name="related-products"></a>Productos relacionados

¿No sabe con seguridad qué solución de aprendizaje automático satisface sus necesidades? Además de análisis incrustado en SQL Server 2016 y 2017 de SQL Server, Microsoft proporciona los siguiente servicios y plataformas de aprendizaje de automático:

+ [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)

  Un entorno multiplataforma para desarrollar, distribuir y administrar los trabajos de aprendizaje de máquina
+ [Data Science Virtual Machine](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview)

  Todas las herramientas que necesita para el aprendizaje automático, preinstalado. Utilizar blocs de notas Jupyter, Python o R.
  
  Probar el nuevo [edition de la vista previa de Windows 2016](http://aka.ms/dsvm/win2016), incluidas las versiones GPU de marcos de trabajo de aprendizaje profundo populares como CNTK y mxNet, así como compatibilidad con contenedores de Windows.
+ [Servicios de Azure cognitivos](https://azure.microsoft.com/services/cognitive-services/)

  Una variedad de servicios en la nube para agregar AI y aprendizaje automático en las aplicaciones, incluidos la indización de lenguaje natural de reconocimiento facial, vídeo, detección de emociones, análisis de texto, traducción, equipo y mucho más
+ [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)

  Una interfaz de arrastrar y colocar en la nube para diseñar flujos de trabajo de aprendizaje de máquina, junto con la capacidad de automatizar e integrar con las aplicaciones a través de servicios web y PowerShell

## <a name="see-also"></a>Vea también

[R Server independiente](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone)

