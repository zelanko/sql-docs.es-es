---
title: Configuración de la migración de datos (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7ad5dddac98c6d70f94f22ba268c890de162bcc3
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779161"
---
# <a name="data-migration-settings-sybasetosql"></a>Configuración de la migración de datos (SybaseToSQL)
  
## <a name="data-migration-settings"></a>Configuración de la migración de datos  
**Configuración de la migración de datos** permite al usuario escribir consultas personalizadas para la migración de datos.  
  
-   Esta pestaña está disponible cuando **opciones de migración de datos ampliado** está establecido en **mostrar** y se oculta cuando el valor está establecido en **ocultar** en configuración del proyecto. Para obtener más información acerca de la configuración del proyecto de migración, consulte [configuración del proyecto (migración)](http://msdn.microsoft.com/en-us/82f8857f-7ab1-4738-ab6e-b1e95ea94924) .  
  
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
[Migrar datos de Sybase a SQL Server o SQL Azure](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811)  
  
