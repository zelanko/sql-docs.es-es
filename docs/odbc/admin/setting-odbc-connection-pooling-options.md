---
title: Configuración de las opciones de agrupación de conexiones ODBC ( ODBC Connection Pooling Options) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1d8e66c506518b77320347ce9120254aa1cae287
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307205"
---
# <a name="setting-odbc-connection-pooling-options"></a>Establecer opciones de agrupación de conexiones ODBC
La agrupación de conexiones permite a una aplicación utilizar una conexión desde un grupo de conexiones que no es necesario restablecer para cada uso. Puede usar la pestaña Agrupación de **conexiones** del cuadro de diálogo Administrador de **orígenes** de datos ODBC para habilitar y deshabilitar la supervisión del rendimiento. Haga doble clic en un nombre de controlador para establecer el período de tiempo de espera de conexión.  
  
 En el nivel de controlador, la agrupación de conexiones está habilitada por el valor del Registro CPTimeout. Esta habilitación selectiva por controlador permite a un administrador del sistema habilitar la agrupación de conexiones solo para los controladores que pueden admitirla. Se logra estableciendo el valor predeterminado de CPTimeout durante el programa de instalación del controlador. Haga doble clic en un nombre de controlador para establecer el período de tiempo de espera de conexión.  
  
 Para obtener más información acerca de la agrupación de conexiones, vea Agrupación de [conexiones ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Supervisión de rendimiento  
 La supervisión del rendimiento realiza un seguimiento del rendimiento de la conexión mediante el registro de una variedad de estadísticas. El desarrollador puede personalizar estas estadísticas para incluir elementos como los siguientes:  
  
|Contador|Definición|  
|-------------|----------------|  
|Contador de conexión rígida ODBC por segundo|El número de conexiones reales por segundo que se realizan al servidor. La primera vez que su entorno lleva una carga pesada, este contador subirá muy rápidamente. Después de unos segundos, caerá a cero. Esta es la situación normal cuando la agrupación de conexiones está funcionando. Cuando se hayan establecido las conexiones con el servidor, se utilizarán y se colocarán en el grupo para su reutilización.|  
|Contador de desconexión dura ODBC por segundo|El número de desconexiones duras por segundo emitidas al servidor. Estas son conexiones reales al servidor que se liberan mediante la agrupación de conexiones. Este valor aumentará de cero cuando detenga todos los clientes en el sistema y las conexiones comiencen a agotar el tiempo de espera.|  
|Contador de conexión suave ODBC por segundo|El número de conexiones satisfechas por el grupo por segundo en otras palabras, conexiones de ese grupo que se entregaron a los usuarios. Este contador indica si la agrupación está funcionando. Dependiendo de la carga en su servidor, no es raro que esto muestre 40-60 conexiones blandas por segundo.|  
|Contador de desconexión suave ODBC por segundo|El número de desconexiones por segundo emitidas por las aplicaciones. Cuando la aplicación se libera o se desconecta, la conexión se vuelve a colocar en el grupo.|  
|Contador de conexión activa actual ODBC|El número de conexiones en el grupo que están actualmente en uso.|  
|Contador de conexión libre actual ODBC|El número actual de conexiones gratuitas disponibles en el grupo. Estas son conexiones en vivo que están disponibles para su uso.|  
|Piscinas actualmente activas|El número de agrupaciones actualmente activas. Este contador se agregó en Windows 8, para los controladores que administran las conexiones en el grupo de conexiones. Para obtener más información, consulte Agrupación de [conexiones compatible con controladores](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Piscinas creadas|El número de agrupaciones activas, incluidos los grupos activos y eliminados. Este contador se agregó en Windows 8, para los controladores que administran las conexiones en el grupo de conexiones. Para obtener más información, consulte Agrupación de [conexiones compatible con controladores](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Debe especificar sus propios parámetros de supervisión. Se han incluido ejemplos para la supervisión del rendimiento con esta versión de ODBC.
