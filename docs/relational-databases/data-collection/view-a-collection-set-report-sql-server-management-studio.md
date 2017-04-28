---
title: "Ver un informe de conjunto de recopilación (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dc.reporthistory.calendar.f1
helpviewer_keywords:
- collection sets [SQL Server], viewing reports
- reports [SQL Server], viewing collection set
ms.assetid: c3b1e791-9aa1-4bba-9622-4954568e1820
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: accee6b8a77439781776f82d179a2260d3aa2895
ms.lasthandoff: 04/11/2017

---
# <a name="view-a-collection-set-report-sql-server-management-studio"></a>Ver un informe de conjunto de recopilación (SQL Server Management Studio)
  Después de haber configurado el almacén de administración de datos, puede ver un informe de conjunto de recopilación en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se proporcionan informes para los conjuntos de recopilación de datos del sistema que se instalan durante el proceso de instalación. Entre otros, se incluyen los siguientes informes:  
  
-   Resumen de uso de disco  
  
-   Historial de estadísticas de consultas  
  
-   Historial de actividad del servidor  
  
 En este procedimiento se muestra el informe para el conjunto de recopilación **Uso de disco** . Puede seguir el mismo procedimiento general para ver los informes de los demás conjuntos de recopilación de datos del sistema.  
  
### <a name="to-view-a-collection-set-report"></a>Para ver un informe de conjunto de recopilación  
  
1.  Las tablas para un informe se crean la primera vez que se cargan los datos recopilados. Si intenta ver un informe antes de esta primera carga, se produce un error y no se muestra ningún informe. Para cargar los datos para el conjunto de recopilación Uso de disco, en Explorador de objetos, expanda la carpeta **Administración** , expanda **Recopilación de datos**y **Conjuntos de recopilación de datos del sistema**, haga clic con el botón derecho en el conjunto de recopilación **Uso de disco** y, después, haga clic en **Recopilar y cargar ahora**.  
  
2.  Para ver el informe, en el Explorador de objetos, expanda la carpeta **Administración** , haga clic con el botón derecho en **Recopilación de datos**, seleccione **Informes**, **Almacén de administración de datos**y, después, haga clic en **Resumen de uso de disco**.  
  
    > [!NOTE]  
    >  Algunos informes pueden mostrar un botón de calendario en la escala de tiempo de la recopilación de datos. Haga clic en este botón para acceder a **Calendario de informe de recopilación de datos**.  
  
#### <a name="data-collection-report-calendar"></a>Calendario de informe de recopilación de datos  
 Utilice este cuadro de diálogo para especificar la fecha de inicio, hora de inicio y duración de los datos que desea notificar. Por ejemplo, puede desear notificar la actividad de uso del disco de un servidor durante un período de 12 horas concreto del último miércoles.  
  
 **Fecha de inicio**  
 Escriba una fecha de inicio para los datos del informe o seleccione una en el calendario.  
  
 **Hora de inicio**  
 Escriba una hora inicial para los datos del informe o especifique una haciendo clic en las flechas.  
  
 **Duración**  
 Especifique el intervalo de tiempo que incluir en el informe. El valor predeterminado es de 240 minutos. Los valores posibles entre los que seleccionar son 15 minutos, 60 minutos, 240 minutos (4 horas), 720 minutos (12 horas) y 1440 minutos (24 horas).  
  
## <a name="see-also"></a>Vea también  
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [Informes personalizados en Management Studio](http://msdn.microsoft.com/library/1ba3f758-f39b-4f5f-91ca-516cedc78979)   
 [Configurar el almacén de administración de datos &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
