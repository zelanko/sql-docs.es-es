---
title: "Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: dcd06bcdf2fbfbb4aaa405c77429c4bd1ffb2448
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages"></a>Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR

Este tutorial muestra cómo utilizar los paquetes de R mejorados proporcionados en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para trabajar con datos de SQL Server y crear soluciones escalables de R, usando el servidor como un contexto de proceso de análisis de macrodatos de alto rendimiento.

Obtendrá información sobre cómo crear un contexto de proceso remoto, mover datos entre los contextos de proceso local y remoto y ejecutar código R en un servidor SQL remoto. También obtendrá información sobre cómo analizar y trazar datos tanto local como en el servidor remoto y cómo crear e implementar modelos.

> [!NOTE]
> 
> Este tutorial funciona específicamente con datos de SQL Server en Windows y usa contextos de proceso en bases de datos. Si desea usar R en otros contextos, como Teradata, Linux o Hadoop, consulte estos tutoriales de Microsoft R Server: 
> + [Usar el servidor de R con sparklyr](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-spark-interop)
> + [Explore R and ScaleR in 25 Functions](https://msdn.microsoft.com/microsoft-r/microsoft-r-tutorial-r2revoscaler) (Explorar R y ScaleR en 25 funciones)
> + [Empezar a trabajar con ScaleR en Hadoop MapReduce](https://msdn.microsoft.com/microsoft-r/scaler-hadoop-getting-started)
> + [Guía de introducción de RevoScaleR Teradata obtener](https://msdn.microsoft.com/microsoft-r/scaler-teradata-getting-started)

## <a name="overview"></a>Información general

Para ilustrar la flexibilidad y la potencia de procesamiento de los paquetes ScaleR, moverá datos e intercambiará contextos de cálculo frecuentemente en este tutorial.

+ Los datos se han obtenido inicialmente de archivos CSV o archivos XDF. Importará los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando las funciones del paquete RevoScaleR.
+ El entrenamiento de modelos y la puntuación se realizarán en el contexto de cálculo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
    Creará nuevas tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usando las funciones **rx** , para guardar los resultados de puntuación.
+ Creará trazados tanto en el servidor como en el contexto de cálculo local.
+ Para entrenar el modelo, usará datos que ya están guardados en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Todos los cálculos se realizarán en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
+ Extraerá un subconjunto de datos y lo guardará como un archivo XDF para volver a usarlo en el análisis en su estación de trabajo local.
+ Los nuevos datos que se usan durante el proceso de puntuación se extraen de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una conexión ODBC. Todos los cálculos se realizan en la estación de trabajo local.
+ Por último, realizará una simulación basada en una función de R personalizada, mediante el contexto de cálculo del servidor.

### <a name="get-started-now"></a>Comenzar ahora

Este tutorial tarda unos 75 minutos en completarse, sin incluir el programa de instalación.

1. [Trabajar con datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [Consultar y modificar los datos de SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [Definir y utilizar los contextos de proceso](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [Crear y ejecutar Scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [Visualizar datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [Crear modelos de R](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [Nuevos datos de puntuación](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [Transformar datos mediante R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [Cargar datos en memoria mediante rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [Crear nueva tabla de SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [Realizar análisis de fragmentación con rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [Analizar los datos de contexto de proceso Local;](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [Mover datos entre SQL Server y el archivo xdf.](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [Cree una simulación Simple](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>Público de destino

Este tutorial está destinado a científicos de datos o a usuarios que ya están familiarizados de alguna manera con R y con las tareas de ciencia de datos incluida la exploración, los análisis estadísticos y la optimización de modelos.  Sin embargo, se proporciona todo el código, por lo que incluso si está familiarizado con R, puede ejecutar el código fácilmente y seguir el tutorial, suponiendo que dispone de los entornos de cliente y servidor necesarios.

También debe estar familiarizado con la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] y saber cómo obtener acceso a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] u otras herramientas de base de datos como Visual Studio.
  
> [!TIP]
> Guarde el área de trabajo de R entre lecciones para que pueda seguir fácilmente desde donde se ha quedado.

### <a name="prerequisites"></a>Requisitos previos

- **SQL Server con compatibilidad con R**
  
    Instalar SQL Server 2016 y habilitar los servicios de R (en bases de datos). O bien, instale SQL Server 2017 y habilitar los servicios de aprendizaje de máquina y elija el lenguaje R. Se describe el proceso de instalación en [libros en pantalla de SQL Server 2016](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx).
  
-  **Permisos de base de datos**
  
    Para ejecutar las consultas usadas para entrenar el modelo, debe tener privilegios **db_datareader** en la base de datos donde se almacenan los datos. Para ejecutar R, el usuario debe tener el permiso EXECUTE ANY EXTERNAL SCRIPT.

-   **Equipo de desarrollo de ciencia de datos**
  
    También debe instalar los paquetes de RevoScaleR y los proveedores relacionados en el entorno de desarrollo de R. La manera más fácil de hacerlo es instalar Microsoft R Client o Microsoft R Server (independiente). Para obtener más información, consulte [Configurar un cliente de ciencia de datos](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx).
      
    > [!NOTE] 
    > No se admiten otras versiones de Revolution R Enterprise o Revolution R Open.
    > 
    > Una distribución de código abierto de R, como R 3.2.2, no funcionará en este tutorial, porque solo las funciones de RevoScaleR pueden usar contextos de proceso remoto.
  
-   **Paquetes adicionales de R**
  
    Para este tutorial, debe instalar los siguientes paquetes: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**y **e1071**. Se proporcionan instrucciones como parte del tutorial.
  
    Todos los paquetes deben estar instalados en dos lugares: en el equipo que utilice para el desarrollo de soluciones de R y en el equipo de SQL Server donde se va a ejecutar scripts de R. Si no tiene permiso para instalar paquetes en el equipo del servidor, pida a un administrador. **No instale los paquetes en una biblioteca de usuario.** Es importante que los paquetes se instalarán en la biblioteca de paquetes de R que se usa por la instancia de SQL Server.

Para obtener más información, consulte [requisitos previos para los tutoriales de ciencia de datos](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).



## <a name="next-step"></a>Paso siguiente

[Trabajar con datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

