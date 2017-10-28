---
title: "Configuración de la migración de datos (DB2ToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 573e673e-a194-4cb2-9aba-aaac6e1a225c
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b1800689474a5ae525dedfff24bab2e60459caba
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="data-migration-settings-db2tosql"></a>Configuración de la migración de datos (DB2ToSQL)
  
## <a name="data-migration-settings"></a>Configuración de la migración de datos  
**Configuración de la migración de datos** permite al usuario escribir consultas personalizadas para la migración de datos.  
  
-   Esta pestaña está disponible cuando **opciones de migración de datos ampliado** está establecido en **mostrar** y se oculta cuando el valor está establecido en **ocultar** en configuración del proyecto. Para obtener más información acerca de la configuración del proyecto de migración, consulte [configuración del proyecto (migración)](http://msdn.microsoft.com/en-us/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae) .  
  
-   Análisis de instrucciones SQL personalizada que se implementará en **configuración de la migración de datos** ficha del nodo de la tabla.  
  
-   Siguientes son las dos casillas de verificación disponibles en la **configuración de la migración de datos** especialmente.:  
  
    1.  Puede truncar la tabla de SQL Server  
  
    2.  Seleccione uso personalizado  
  
1.  **Puede truncar la tabla de SQL Server:**  
     Esta opción permite al usuario tener una visión clara de los datos migrados en la base de datos de destino.  
  
    -   De forma predeterminada, este cuadro de texto está activada.  
  
    -   Si este cuadro de texto no está activada, los datos que se migren se agregará a los datos existentes en la base de datos de destino.  
  
2.  **Seleccione uso personalizado:**  
     Esta opción permite al usuario modificar el **seleccione** instrucción presente (**seleccione** instrucción permite a los usuarios seleccionar los datos que se mostrará en la base de datos de destino).  
  
    1.  De forma predeterminada, este cuadro de texto está desactivada.  
  
    2.  Si se activa este cuadro de texto, que permite a los usuarios modificar la **seleccione** instrucción está presente.  
  
Hay dos botones presentes lleve.:  
  
-   **Aplicar:** haga clic en **aplicar** para aplicar la configuración que se han cambiado.  
  
-   **Cancelar:** haga clic en **cancelar** para restaurar la configuración está presente antes de que se realizaron los cambios.  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de DB2 a SQL Server](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b)  
  

