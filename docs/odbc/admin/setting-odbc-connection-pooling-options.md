---
description: Establecer opciones de agrupación de conexiones ODBC
title: Establecer opciones de agrupación de conexiones ODBC | Microsoft Docs
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
ms.openlocfilehash: 5d6f741654f9765e909a8a2e33bce5e7e596f8b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386601"
---
# <a name="setting-odbc-connection-pooling-options"></a>Establecer opciones de agrupación de conexiones ODBC
La agrupación de conexiones permite a una aplicación utilizar una conexión de un grupo de conexiones que no es necesario restablecer para cada uso. Puede usar la pestaña **agrupación de conexiones** del cuadro de diálogo **Administrador de orígenes de datos ODBC** para habilitar y deshabilitar la supervisión de rendimiento. Haga doble clic en un nombre de controlador para establecer el período de tiempo de espera de la conexión.  
  
 En el nivel de controlador, el valor del registro CPTimeout habilita la agrupación de conexiones. Esta habilitación selectiva por controlador permite a un administrador del sistema habilitar la agrupación de conexiones solo para los controladores que lo admiten. Para lograrlo, se establece el valor predeterminado de CPTimeout durante el programa de instalación del controlador. Haga doble clic en un nombre de controlador para establecer el período de tiempo de espera de la conexión.  
  
 Para obtener más información sobre la agrupación de conexiones, vea [agrupación de conexiones ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Supervisión de rendimiento  
 La supervisión del rendimiento realiza un seguimiento del rendimiento de la conexión mediante la grabación de diversas estadísticas. El desarrollador puede personalizar estas estadísticas para incluir elementos como los siguientes:  
  
|Contador|Definición|  
|-------------|----------------|  
|Contador de conexión de disco duro ODBC por segundo|El número de conexiones reales por segundo que se realizan en el servidor. La primera vez que el entorno lleve una carga pesada, este contador se activará con mucha rapidez. Después de unos segundos, se quitará de cero. Esta es la situación normal cuando funciona la agrupación de conexiones. Cuando se hayan establecido las conexiones con el servidor, se usarán y se colocarán en el grupo para su reutilización.|  
|Contador de desconexión de hardware de ODBC por segundo|Número de desconexiones difíciles por segundo emitidas al servidor. Son conexiones reales con el servidor que se están liberando mediante la agrupación de conexiones. Este valor aumentará de cero al detener todos los clientes del sistema y las conexiones comenzarán a agotar el tiempo de espera.|  
|Contador de conexiones de software ODBC por segundo|El número de conexiones que cumple el grupo por segundo, es decir, las conexiones de ese grupo que se han entregado a los usuarios. Este contador indica si la agrupación funciona. En función de la carga del servidor, no es raro que esto muestre 40-60 conexiones de software por segundo.|  
|Contador de desconexión temporal de ODBC por segundo|Número de desconexiones por segundo emitidas por las aplicaciones. Cuando la aplicación se libera o se desconecta, la conexión se vuelve a colocar en el grupo.|  
|Contador de conexión activa de ODBC actual|El número de conexiones en el grupo que están actualmente en uso.|  
|Contador de conexión libre actual ODBC|Número actual de conexiones libres disponibles en el grupo. Son conexiones dinámicas que están disponibles para su uso.|  
|Grupos activos actualmente|Número de grupos activos actualmente. Este contador se agregó en Windows 8 para los controladores que administran las conexiones en el grupo de conexiones. Para obtener más información, consulte [agrupación de conexiones compatible con controladores](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Grupos creados|El número de grupos activos, incluidos los grupos activos y eliminados. Este contador se agregó en Windows 8 para los controladores que administran las conexiones en el grupo de conexiones. Para obtener más información, consulte [agrupación de conexiones compatible con controladores](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Debe especificar sus propios parámetros de supervisión. En esta versión de ODBC se han incluido ejemplos de supervisión de rendimiento.
