---
title: "Establecer opciones de agrupación de conexiones ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: admin
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d44325018516574641ccb938a8d7acbefb121cd4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="setting-odbc-connection-pooling-options"></a>Establecer opciones de agrupación de conexiones ODBC
Agrupación de conexiones permite a una aplicación que utilice una conexión de un grupo de conexiones que no es necesario que restablecerse para cada usuario. Puede usar el **agrupación de conexiones** pestaña de la **Administrador de orígenes de datos ODBC** cuadro de diálogo para habilitar y deshabilitar la supervisión de rendimiento. Haga doble clic en un nombre de controlador para establecer el período de tiempo de espera de conexión.  
  
 En el nivel de controlador, la agrupación de conexiones está habilitada por el valor de registro CPTimeout. Esta habilitación selectiva por controlador permite que un administrador del sistema habilitar la agrupación de conexiones para solo los controladores que lo admiten. Se realiza estableciendo el valor predeterminado de CPTimeout durante el programa de instalación del controlador. Haga doble clic en un nombre de controlador para establecer el período de tiempo de espera de conexión.  
  
 Para obtener más información acerca de la agrupación de conexiones, vea [agrupación de conexiones ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Supervisión de rendimiento  
 Supervisión de rendimiento realiza el seguimiento de rendimiento de la conexión mediante la grabación de una variedad de estadísticas. Estas estadísticas se pueden personalizar el programador para incluir elementos como las siguientes:  
  
|Contador|Definición|  
|-------------|----------------|  
|Contador de disco duro de conexión de ODBC por segundo|El número real de conexiones por segundo que se realizan en el servidor. La primera vez que su entorno conlleva una carga pesada, este contador se Subir muy rápidamente. Después de unos segundos, se quitará a cero. Esta es la situación normal cuando la agrupación de conexiones está funcionando. Cuando se han establecido las conexiones al servidor, se usa y se coloca en el grupo para su reutilización.|  
|Disco duro de ODBC desconectar contador por segundo|El número de disco duro desconexiones por segundo que se emiten al servidor. Se trata de conexiones reales en el servidor que se publica la agrupación de conexiones. Este valor aumentará de cero cuando detenga a todos los clientes en el sistema y las conexiones comienzan a tiempo de espera.|  
|Contador de software de conexión de ODBC por segundo|El número de conexiones satisfechos por el grupo por segundo, en otras palabras, las conexiones de ese grupo que se va a pasar a los usuarios. Este contador indica si la agrupación está funcionando. Dependiendo de la carga en el servidor, no es raro que esta opción para mostrar las conexiones de software de 40 y 60 por segundo.|  
|Contador de desconexión automáticos de ODBC por segundo|El número de desconexiones por segundo emitido por las aplicaciones. Cuando la aplicación se libera o se desconecta, la conexión se coloca en el grupo.|  
|Contador de conexión activa actual de ODBC|El número de conexiones en el grupo que están actualmente en uso.|  
|Contador actual de conexión libre de ODBC|El número actual de conexiones libres disponibles en el grupo. Estas son las conexiones activas que están disponibles para su uso.|  
|Los grupos de activas actualmente|El número de agrupaciones activas actualmente. Este contador se agregó en Windows 8, para controladores que administran las conexiones del grupo de conexiones. Para obtener más información, consulte [agrupación de conexiones dependientes del controlador](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Grupos creados|El número de activos, incluidos los grupos de activos y se quitan de grupos. Este contador se agregó en Windows 8, para controladores que administran las conexiones del grupo de conexiones. Para obtener más información, consulte [agrupación de conexiones dependientes del controlador](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Debe especificar sus propios parámetros de supervisión. Ejemplos de supervisión del rendimiento se han incluido con esta versión de ODBC.
