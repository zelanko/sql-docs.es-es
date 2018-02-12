---
title: 'Profundidad de ciencia de datos: mediante los paquetes de RevoScaleR con SQL Server | Documentos de Microsoft'
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 003434a055ab73afb288ea5801130ce1c06aa9c5
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages-with-sql-server"></a>Profundidad de ciencia de datos: mediante los paquetes de RevoScaleR con SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tutorial muestra cómo utilizar los paquetes de R mejorados proporcionados en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para trabajar con datos de SQL Server y crear soluciones escalables de R, usando el servidor como un contexto de proceso de análisis de macrodatos de alto rendimiento.

Obtenga información acerca de cómo crear un contexto de proceso remoto, mover datos entre los contextos de proceso local y remoto y ejecutar código R en un servidor SQL remoto. También aprenderá cómo analizar y trazar datos tanto local como en el servidor remoto y cómo crear e implementar modelos.

> [!NOTE]
> 
> Este tutorial funciona específicamente con datos de SQL Server en Windows y usa contextos de proceso en bases de datos. Si desea usar R en otros contextos, como Teradata, Linux o Hadoop, consulte estos tutoriales de Microsoft R Server: 
> + [Usar el servidor de R con sparklyr](https://docs.microsoft.com/machine-learning-server/r/tutorial-sparklyr-revoscaler)
> + [Explore R and ScaleR in 25 Functions](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler) (Explorar R y ScaleR en 25 funciones)
> + [Empezar a trabajar con ScaleR en Hadoop MapReduce](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-hadoop)

## <a name="overview"></a>Información general

Para experimentar la flexibilidad y potencia de procesamiento del paquete RevoScaleR, en este tutorial, mover datos e intercambio de contextos de proceso con frecuencia. Para ilustrar, estas son algunas de las tareas en este tutorial:

+ Los datos se han obtenido inicialmente de archivos CSV o archivos XDF. Importar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante las funciones en el paquete RevoScaleR.
+ Modelo de entrenamiento y de puntuación se realizan utilizando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de proceso. 
+ Usar funciones de RevoScaleR para crear nuevos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas para guardar los resultados de puntuación.
+ Crear gráficos tanto en el servidor y en el equipo local el contexto de proceso.
+ Entrenar un modelo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos, ejecutar código R el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.
+ Extraer un subconjunto de datos y lo guarda como un archivo xdf. para volver a usar en el análisis en la estación de trabajo local.
+ Obtener nuevos datos para puntuación, abriendo una conexión ODBC a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. La puntuación se realiza en la estación de trabajo local.
+ Crear una función de R personalizada y lo ejecuta en el servidor de contexto de proceso para realizar una simulación.

### <a name="article-list-and-time-required"></a>Lista de artículos y el tiempo requerido

Este tutorial tarda unos 75 minutos en completarse, sin incluir el programa de instalación.

1. [Trabajar con datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [Consultar y modificar los datos de SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [Definir y usar contextos de cálculo](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [Crear y ejecutar Scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [Visualizar datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [Crear modelos de R](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [Nuevos datos de puntuación](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [Transformar datos mediante R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [Cargar datos en memoria mediante rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [Crear nuevas tablas de SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [Realizar análisis de fragmentación mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [Analizar datos en el contexto del proceso local](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [Mover los datos de SQL Server con archivos xdf.](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [Crear una simulación sencilla](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>Audiencia de destino

Este tutorial está pensado para científicos de datos o para las personas que ya están un poco familiarizado con R y con tareas de ciencia de datos como resúmenes y creación de modelos.  Sin embargo, se proporciona todo el código, por lo que incluso si está familiarizado con R, puede ejecutar el código y seguir el tutorial, suponiendo que dispone de los entornos de cliente y servidor necesarios.

También debe estar familiarizado con [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis y saber cómo obtener acceso a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos mediante herramientas como los siguientes:

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Herramientas de base de datos en Visual Studio 
+ Gratuitamente [mssql extensión para Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).
  
> [!TIP]
> Guarde el área de trabajo de R entre lecciones para que pueda seguir fácilmente desde donde se ha quedado.

### <a name="prerequisites"></a>Requisitos previos

- **SQL Server con compatibilidad con R**
  
    Instalar SQL Server 2016 y habilitar los servicios de R (en bases de datos). O bien, instale SQL Server 2017 y habilitar los servicios de aprendizaje de máquina y elija el lenguaje R.
  
-  **Permisos de base de datos**
  
    Para ejecutar las consultas usadas para entrenar el modelo, debe tener privilegios **db_datareader** en la base de datos donde se almacenan los datos. Para ejecutar R, el usuario debe tener el permiso EXECUTE ANY EXTERNAL SCRIPT.

-   **Equipo de desarrollo de ciencia de datos**
  
    Debe instalar los paquetes de RevoScaleR y los proveedores relacionados en el equipo que se usa como el entorno de desarrollo de R. La manera más fácil de hacerlo consiste en instalar cliente de R de Microsoft, Microsoft R Server (independiente) o servidor de aprendizaje de máquina (independiente). 
      
    > [!NOTE] 
    > No se admiten otras versiones de Revolution R Enterprise o Revolution R Open.
    > 
    > No se puede usar una distribución de código abierto de R en este tutorial, dado que solo las funciones de RevoScaleR pueden usar contextos de proceso remoto.
  
-   **Paquetes adicionales de R**
  
    En este tutorial, instalar los siguientes paquetes: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**, y **e1071** . Se proporcionan instrucciones como parte del tutorial.
  
    Todos los paquetes deben estar instalados en dos lugares: en el equipo que utilice para el desarrollo de soluciones de R y en el equipo de SQL Server donde se ejecutan los scripts de R. Si no tiene permiso para instalar paquetes en el equipo del servidor, pida a un administrador. 
    
    **No instale los paquetes en una biblioteca de usuario.** Los paquetes deben instalarse en la biblioteca de paquetes de R que se usa por la instancia de SQL Server.

Para obtener más información, consulte [requisitos previos para los tutoriales de ciencia de datos](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

## <a name="next-step"></a>Paso siguiente

[Trabajar con datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

