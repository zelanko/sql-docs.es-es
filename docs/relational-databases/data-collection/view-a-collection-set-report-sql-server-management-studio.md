---
description: Ver un informe de conjunto de recopilación (SQL Server Management Studio)
title: Visualización de un informe de conjunto de recopilación (SSMS)
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.reporthistory.calendar.f1
helpviewer_keywords:
- collection sets [SQL Server], viewing reports
- reports [SQL Server], viewing collection set
ms.assetid: c3b1e791-9aa1-4bba-9622-4954568e1820
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5132dc4b782cb9af8e5e096ae35f57d8266a27c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487233"
---
# <a name="view-a-collection-set-report-sql-server-management-studio"></a>Ver un informe de conjunto de recopilación (SQL Server Management Studio)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
 **Duration**  
 Especifique el intervalo de tiempo que incluir en el informe. El valor predeterminado es 240 minutos. Los valores posibles entre los que seleccionar son 15 minutos, 60 minutos, 240 minutos (4 horas), 720 minutos (12 horas) y 1440 minutos (24 horas).  
  
## <a name="see-also"></a>Consulte también  
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [Informes personalizados en Management Studio](../../ssms/object/custom-reports-in-management-studio.md)   
 [Configurar el almacén de administración de datos &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
