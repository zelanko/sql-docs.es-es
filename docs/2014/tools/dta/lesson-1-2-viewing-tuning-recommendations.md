---
title: Ver recomendaciones de optimización | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: e4e690c9-434f-4b01-b4de-0b905323ddd6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe8d52d898db35698155518646f074e7167687a0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66110176"
---
# <a name="viewing-tuning-recommendations"></a>Ver recomendaciones de optimización
   En esta tarea, se utiliza la sesión de optimización que creó en [Optimizar una carga de trabajo](lesson-1-1-tuning-a-workload.md). Después [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] de optimizar la base de datos mediante el script de script. [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL, [!INCLUDE[ssDE](../../includes/ssde-md.md)] el Asistente para la optimización de muestra los resultados en la pestaña **recomendaciones** . La siguiente tarea presenta la pestaña **recomendaciones** de la [!INCLUDE[ssDE](../../includes/ssde-md.md)] interfaz gráfica de usuario (GUI) del Asistente para la optimización de y le guía para explorar la información que proporciona sobre los resultados de la sesión de optimización.  
  
### <a name="view-tuning-recommendations"></a>Ver las recomendaciones de optimización  
  
1.  Inicie el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Consulte [Iniciar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md). Asegúrese de conectarse a la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha usado en la práctica [Optimizar una carga de trabajo](lesson-1-1-tuning-a-workload.md).  
  
2.  Haga doble clic en **MySession** en el panel **Monitor de sesión** . [!INCLUDE[ssDE](../../includes/ssde-md.md)]Carga la información de sesión de la sesión de optimización anterior y muestra la **pestaña recomendaciones** . tenga en [!INCLUDE[ssDE](../../includes/ssde-md.md)] cuenta que el Asistente para la optimización de no realizó **recomendaciones de partición** porque aceptó todos los valores predeterminados de la opción de optimización y no se ha seleccionado **ninguna partición** en la pestaña **Opciones de optimización** .  
  
3.  En la pestaña **Recomendaciones** , utilice la barra de desplazamiento situada en la parte inferior de la página con pestañas para ver todas las columnas de **Recomendaciones de índices** . Cada fila representa un objeto de base de datos (índices o vistas indizadas) que el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] recomienda quitar o crear. Desplácese hasta la columna situada más a la derecha y haga clic en **Definición**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] muestra la ventana **Vista previa de script SQL** , donde se puede ver el script [!INCLUDE[tsql](../../includes/tsql-md.md)] que creará o quitará el objeto de base de datos de esa fila. Haga clic en **Cerrar** para cerrar la ventana de vista previa.  
  
     Si le resulta difícil encontrar una **Definición** que contenga un vínculo, haga clic para desactivar la casilla **Mostrar objetos existentes** al final de la página con pestañas. Esto hará que el número de filas mostradas disminuya. Cuando desactive esta casilla, el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] solamente mostrará los objetos para los que haya generado una recomendación. Active la casilla **Mostrar objetos existentes** para ver todos los objetos de base de datos que existen actualmente en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Utilice la barra de desplazamiento situada en la parte derecha de la página con pestañas para ver todos los objetos.  
  
4.  Haga clic con el botón derecho en la cuadrícula del panel **Recomendaciones de índices** . Este menú contextual permite seleccionar y anular la selección de recomendaciones. También permite cambiar la fuente del texto de la cuadrícula.  
  
5.  En el menú **Acciones** , haga clic en **Guardar recomendaciones** para guardar todas las recomendaciones en un script [!INCLUDE[tsql](../../includes/tsql-md.md)] . Llame `MySessionRecommendations.sql` al script.  
  
     Abra el script MySessionRecommendations.sql en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para verla. Podría aplicar las recomendaciones a la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ejecutando el script en el Editor de consultas; pero no lo haga. Cierre el script en el Editor de consultas sin ejecutarla.  
  
     También podría aplicar las recomendaciones haciendo clic en **Aplicar recomendaciones** en el menú **Acciones** del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] ; pero no lo haga en esta práctica.  
  
6.  Si hay más de una recomendación en la pestaña **Recomendaciones** , borre algunas de las filas que enumeran objetos de base de datos en la cuadrícula **Recomendaciones de índices** .  
  
7.  En el menú **Acciones** , haga clic en **Evaluar recomendaciones**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] crea una nueva sesión de optimización en la que puede evaluar un subconjunto de las recomendaciones originales de MySession.  
  
8.  Escriba `EvaluateMySession` para el nuevo **nombre de sesión**y haga clic en el botón **Iniciar análisis** de la barra de herramientas. Puede repetir los pasos 2 y 3 con esta nueva sesión de optimización para ver las recomendaciones.  
  
## <a name="summary"></a>Resumen  
 Ha visto el contenido de la pestaña **Recomendaciones** para la sesión de optimización MySession y ha evaluado un subconjunto de recomendaciones en la nueva sesión de optimización EvaluateMySession.  
  
 Evaluar un subconjunto de recomendaciones de optimización puede ser necesario si tiene que cambiar las opciones de optimización después de ejecutar una sesión. Por ejemplo, si solicita al Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que tenga en cuenta las vistas indizadas cuando especifique opciones de optimización para una sesión, pero, después de que la recomendación se genere, decide usar las vistas indizadas de nuevo, Después, puede usar la opción **evaluar recomendaciones** del menú **acciones** para que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] Asistente para la optimización de vuelva a evaluar la sesión sin tener en cuenta las vistas indizadas. Cuando utilice la opción **Evaluar recomendaciones** , las recomendaciones generadas previamente se aplicarán hipotéticamente al diseño físico actual para lograr el diseño físico de la segunda sesión de optimización.  
  
 La pestaña **Informes** , que se describe en la siguiente tarea de la lección, muestra más información sobre los resultados de optimización.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Ver informes de optimización](lesson-1-3-viewing-tuning-reports.md)  
  
  
