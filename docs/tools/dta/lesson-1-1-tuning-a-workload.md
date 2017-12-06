---
title: Optimizar una carga de trabajo | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: workloads [SQL Server], tuning
ms.assetid: 6229bf3f-1182-4bc6-8451-cedc37f4b62e
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 56041b15a6fa78bc88d62c409f0df958d0dd862a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-1-1---tuning-a-workload"></a>Lección 1-1-optimizar una carga de trabajo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]El Asistente para la optimización de motor de base de datos puede utilizarse para encontrar el mejor diseño físico de la base de datos de rendimiento de las consultas en las bases de datos y tablas que seleccionó para la optimización.  
  
En esta tarea se usa la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada. Para instalarlas, consulte [Instalar ejemplos de SQL Server y bases de datos de ejemplo](http://sqlserversamples.codeplex.com).  
  
### <a name="tune-a-workload-transact-sql-script-file"></a>Optimizar un archivo de script Transact-SQL de carga de trabajo  
  
1.  Copie una instrucción o instrucciones SELECT de ejemplo de la sección A. Uso de SELECT para recuperar filas y columnas" en [Ejemplos de SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md) y pegue las instrucciones en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Guarde el archivo como **MyScript.sql** en un directorio donde pueda encontrarlo fácilmente.  
  
2.  Inicie el Asistente para la optimización de motor de base de datos. Consulte [Iniciar el Asistente para la optimización de motor de base de datos](../../tools/dta/lesson-1-1-launching-database-engine-tuning-advisor.md).  
  
3.  En el panel derecho de la GUI del Asistente para la optimización de motor de base de datos, escriba **MySession** en **Nombre de sesión**.  
  
4.  Seleccione **Archivo** para la **Carga de trabajo**y, después, haga clic en el botón **Busque un archivo de carga de trabajo** para localizar el archivo **MyScript.sql** que guardó en el paso 1.  
  
5.  Seleccione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en la lista **Base de datos para análisis de carga de trabajo** , seleccione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en la cuadrícula **Seleccionar bases de datos y tablas para optimizar** y deje activada la opción **Guardar registro de optimización** . **Base de datos para análisis de carga de trabajo** especifica la primera base de datos a la que se conecta el Asistente para la optimización de motor de base de datos al optimizar una carga de trabajo. Una vez iniciada la optimización, el Asistente para la optimización de motor de base de datos se conecta a las bases de datos especificadas en las instrucciones `USE DATABASE` que contiene la carga de trabajo.  
  
6.  Haga clic en la pestaña **Opciones de optimización** . En esta práctica, no configurará ninguna opción de optimización, pero tómese unos minutos para revisar las opciones predeterminadas. Presione F1 para ver la Ayuda para esta página con pestañas. Haga clic en **Opciones avanzadas** para ver opciones de optimización adicionales. Haga clic en **Ayuda** , en el cuadro de diálogo **Opciones avanzadas de optimización** , para obtener información sobre las opciones que aparecen. Haga clic en **Cancelar** para cerrar el cuadro de diálogo **Opciones avanzadas de optimización** , y deje seleccionadas las opciones predeterminadas.  
  
7.  Haga clic en el botón **Iniciar análisis** de la barra de herramientas. Mientras el Asistente para la optimización de motor de base de datos analiza la carga de trabajo, puede supervisar el estado en la pestaña **Progreso** . Una vez se haya completado la optimización, aparecerá la pestaña **Recomendaciones**.  
  
    Si recibe un error acerca de la fecha y la hora de detención de la optimización, compruebe el valor de **Detener el** en la pestaña principal de **Opciones de optimización** . Asegúrese de que la fecha y la hora de **Detener el** son posteriores a la fecha y la hora actuales, y cámbielas si resulta necesario.  
  
8.  Una vez completado el análisis, guarde su recomendación como un script de [!INCLUDE[tsql](../../includes/tsql-md.md)] haciendo clic en **Guardar recomendaciones** en el menú **Acciones** . En el cuadro de diálogo **Guardar como** , navegue hasta el directorio en el que quiere guardar el script de recomendaciones y escriba el nombre de archivo **MyRecommendations**.  
  
## <a name="summary"></a>Resumen  
Ha completado la optimización de una carga de trabajo de instrucción SELECT simple en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . El Asistente para la optimización de motor de base de datos también puede utilizar tablas y archivos de seguimiento del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] como cargas de trabajo de optimización. La tarea siguiente muestra cómo ver e interpretar las recomendaciones de optimización que ha recibido tras la optimización de práctica.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Ver recomendaciones de optimización](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md)  
  
  
  
