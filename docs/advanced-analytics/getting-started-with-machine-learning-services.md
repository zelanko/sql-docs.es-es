---
title: "Introducción a aprendizaje automático en SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 12/20/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: a54400e73c7789dcea15cbd4929c2a7878297df5
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2018
---
# <a name="getting-started-with-machine-learning-in-sql-server"></a>Getting started with machine learning in SQL Server (Introducción al aprendizaje automático en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft ofrece un conjunto integrado y escalable de soluciones de aprendizaje automático para local y la nube:

+ **Integrado**, ya que puede ejecutar R o Python en SQL Server. Esto le permite fácilmente procesos de mezcla enterprise para ETL y los informes con datos de tareas de ciencia como característica de ingeniería, creación de modelos y la puntuación.
+ **Escalable**, ya que pueden desarrollar y probar una solución en un equipo portátil y, a continuación, implementarla en varias plataformas para distribuir los científicos de datos o el procesamiento en paralelo de las operaciones de clave como modelo de entrenamiento y de puntuación. Plataformas compatibles incluyen SQL Server en Windows, Hadoop y Spark.

Este artículo contiene vínculos a los recursos de cada producto de la plataforma de aprendizaje automático de Microsoft.

## <a name="machine-learning-in-sql-server"></a>Aprendizaje de SQL Server automático

+ SQL Server 2017

  A partir de SQL Server 2017, ahora puede usar código de Python en SQL Server. Para reflejar la compatibilidad más amplia de las soluciones de varios idiomas (con más proceder!) y el nombre se ha cambiado a [!INCLUDE[rsql-productnamenew-md](../includes/rsql-productnamenew-md.md)]. Ahora puede automatizar tareas de aprendizaje automático mediante las herramientas de SQL para ejecutar código R o Python. O bien, usar el equipo de SQL Server como el _cálculo_ para los trabajos que se inicia desde un entorno de desarrollo remoto.

    + [Introducción a la arquitectura de Python en SQL Server](../advanced-analytics/python/architecture-overview-sql-server-python.md)
    + [Instalar servicios de aprendizaje de 2017 máquinas SQL Server](install/sql-machine-learning-services-windows-install.md)

+ SQL Server 2016

  SQL Server 2016 admite ejecutar código R en SQL Server mediante procedimientos almacenados. Esto facilita la automatizar tareas de aprendizaje automático mediante las herramientas SQL. O bien, puede ejecutar código R desde un portátil remoto o el entorno de desarrollo de R, al usar el equipo de SQL Server como el _cálculo_.

  Esta integración proporciona seguridad para los datos y le permite administrar y equilibrar los recursos que usa R.

    + [Obtener iniciado wth SQL Server R Services](r/getting-started-with-sql-server-r-services.md)
    + [Instalar SQL Server 2016 R Services](install/sql-r-services-windows-install.md)

## <a name="microsoft-machine-learning-server-microsoft-r-server"></a>Microsoft Machine Learning Microsoft R (servidor)

La opción para instalar [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)] se proporciona en SQL Server 2017 para admitir los clientes empresariales que desean ejecutar trabajos de aprendizaje automático distribuida y escalable, pero que no necesitan la integración con el motor de base de datos de SQL Server, como el uso del proceso SQL contextos.

En SQL Server 2016, utilice la opción para instalar [!INCLUDE[rsql-platform-md](../includes/rsql-platformnew-md.md)].
  
  + [Asistente para servidor de aprendizaje automático](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)
  
También puede instalar [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)] o [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)] a través de instaladores específica de la plataforma:

  + [Instalar en Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
  + [Instalar en Linux](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-linux-install)
  + [Instalar en Hadoop](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-hadoop-install)

> [!IMPORTANT]
> Si desea ejecutar Python con R Server, asegúrese de instalar la versión más reciente, [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)], que está disponible sólo a través de [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)] el programa de instalación:
> 
>    + [Instalar servidor de aprendizaje de máquina (independiente) de SQL Server de 2017](install/sql-machine-learning-standalone-windows-install.md) o [instalar SQL Server 2016 R Server (independiente)](install/sql-r-standalone-windows-install.md).

## <a name="related-products"></a>Productos relacionados

+ [Configurar un cliente de ciencia de datos](../advanced-analytics/r/set-up-a-data-science-client.md)

  Si ya ha instalado uno de los productos de servidor de aprendizaje automático, este artículo proporciona información acerca de cómo configurar un equipo independiente para desarrollo y pruebas de soluciones, incluidas las herramientas y bibliotecas necesarias.

+ [Data Science Virtual Machine](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

  Impulsar su entrada en aprendizaje obteniendo esta máquina completa solución de Azure Marketplace de aprendizaje automático. La máquina de virtual de ciencia de datos (con frecuencia abreviada como "DSVM") incluye SQL Server, servidor de aprendizaje de máquina de Microsoft y todas las herramientas de desarrollo.
  
  La versión más reciente de la máquina Virtual de ciencia de datos (DSVM) se ejecuta en Windows 2016 Preview Edition, para proporcionar la apariencia personalizable limpia de Windows 10. Viene preconfigurado con controladores, CUDA Kit de herramientas 8.0 y la biblioteca de cuDNN NVIDIA para cargas de trabajo GPU NVIDIA.

## <a name="resources-for-learning"></a>Recursos de aprendizaje

+ [Tutoriales de aprendizaje de máquina](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)

  Empiece aquí para buscar una lista de todos los recursos para aprender sobre soluciones de aprendizaje de máquina con SQL Server 2016 y 2017 de SQL Server.

### <a name="r-tutorials"></a>Tutoriales de R

+ [Tutoriales de SQL Server R](../advanced-analytics/tutorials/sql-server-r-tutorials.md)

   Obtenga información acerca de cómo ejecutar R en SQL Server, crear y usar contextos de proceso remoto o realizar simulaciones en R mediante SQL Server.
   
   Incluye tutoriales de "todo el código proporcionado" para que pueda ejecutar una solución completa de R desde SQL Server Management Studio, sin tener que abrir alguna vez un IDE de R.

+ [Explorar R y ScaleR en 25 funciones cortas](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

   ¿No está familiarizado con R? ¿Se pregunta cómo Microsoft R (o RevoScaleR) se compara con R estándar? Puede encontrar estos inicia rápida R Server y servidor de aprendizaje de máquina.

### <a name="python-tutorials"></a>Tutoriales de Python

+ [Tutoriales de SQL Server Python](../advanced-analytics/tutorials/sql-server-r-tutorials.md)

  Obtenga información acerca de cómo ejecutar Python en [!INCLUDE[ssnoversion](../includes/ssnoversion.md)]. Genera un modelo con Python y usarlo para puntuar datos de SQL Server.

   Una solución end-to-end para desarrolladores de SQL proporciona todo el código que deba ejecutar Python desde SQL Server Management Studio.


### <a name="product-samples-with-code"></a>Ejemplos del producto con el código

Estas soluciones desde el equipo de desarrollo de SQL Server se ejecutan en R o Python y muestran escenarios comunes para la integración de aprendizaje automático con aplicaciones de negocios.

+ [Compilar una aplicación inteligente con SQL Server y R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

+ [Compilar una aplicación inteligente con SQL Server y Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

### <a name="data-science-solution-templates"></a>Plantillas de solución de ciencia de datos

Las plantillas de solución desde el equipo de ciencia de datos de Microsoft representan adaptadas para industrias específicas o escenarios de soluciones de ejemplo completo. Están destinadas a actuar como bloques de creación para ayudarle a implementar una solución rápida, o para demostrar los procedimientos recomendados. Cada plantilla incluye datos de ejemplo y el código personalizable.

+ [Plantillas de solución](../advanced-analytics/tutorials/data-science-scenarios-and-solution-templates.md)

## <a name="next-steps"></a>Pasos siguientes

[Introducción a servicios de aprendizaje de máquina de SQL Server](../advanced-analytics/r/getting-started-with-sql-server-r-services.md)

[Empezar a trabajar con el servidor de aprendizaje de automático de Microsoft](../advanced-analytics/r/getting-started-with-microsoft-r-server-standalone.md)
