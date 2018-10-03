---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46b6f5d7e6af3726558f5cee72f00ff06e13ab89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812063"
---
# <a name="setting-odbc-connection-pooling-options"></a>Establecer opciones de agrupación de conexiones ODBC
Agrupación de conexiones permite a una aplicación usar una conexión de un grupo de conexiones que no deben establecerse para cada usuario. Puede usar el **agrupación de conexiones** pestaña de la **Administrador de orígenes de datos ODBC** cuadro de diálogo para habilitar y deshabilitar la supervisión de rendimiento. Haga doble clic en un nombre de controlador para establecer el período de tiempo de espera de conexión.  
  
 En el nivel de controlador, la agrupación de conexiones está habilitada por el valor del registro CPTimeout. Esta habilitación selectiva por controlador permite que un administrador del sistema habilitar la agrupación de conexiones para solo los controladores que lo admiten. Se consigue al establecer el valor predeterminado de CPTimeout durante el programa de instalación del controlador. Haga doble clic en un nombre de controlador para establecer el período de tiempo de espera de conexión.  
  
 Para obtener más información acerca de la agrupación de conexiones, vea [agrupación de conexiones ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Supervisión de rendimiento  
 Supervisión de rendimiento realiza el seguimiento de rendimiento de la conexión mediante la grabación de una variedad de estadísticas. Estas estadísticas se pueden personalizar el programador para incluir elementos como los siguientes:  
  
|Contador|Definición|  
|-------------|----------------|  
|Contador de disco duro de conexión de ODBC por segundo|El número real de conexiones por segundo que se realizan en el servidor. La primera vez que el entorno lleva una carga pesada, este contador suban muy rápidamente. Después de unos segundos, caerá hasta cero. Se trata de la situación normal cuando la agrupación de conexiones está funcionando. Cuando se han establecido las conexiones al servidor, se usa y se colocan en el grupo para su reutilización.|  
|Disco duro ODBC desconectar contador por segundo|El número de disco duro desconexiones por segundo que se emiten al servidor. Estas son las conexiones reales en el servidor que se lanzan mediante la agrupación de conexiones. Este valor aumentará desde cero cuando se detiene a todos los clientes en el sistema y las conexiones empiezan a tiempo de espera.|  
|Contador ODBC conexión temporal por segundo|El número de conexiones satisfechos el grupo por segundo, en otras palabras, las conexiones de ese grupo que se va a pasar a los usuarios. Este contador indica si la agrupación está funcionando. Dependiendo de la carga en el servidor, no es raro que esta opción para mostrar 40: 60 conexiones temporalmente por segundo.|  
|Contador de desconexión temporal ODBC por segundo|El número de desconexiones por segundo emitido por las aplicaciones. Cuando la aplicación libera o se desconecta, la conexión se coloca en el grupo.|  
|Contador de conexión activa actual de ODBC|El número de conexiones en el grupo que están actualmente en uso.|  
|Contador actual de conexión libre de ODBC|El número actual de conexiones libres disponibles en el grupo. Estas son las conexiones dinámicas que están disponibles para su uso.|  
|Los grupos actualmente activo|El número de grupos actualmente activos. Este contador se agregó en Windows 8, para los controladores de administración de conexiones en el grupo de conexiones. Para obtener más información, consulte [Driver-Aware Connection Pooling](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Grupos creados|El número de grupos activos, incluidos los grupos activos y eliminados. Este contador se agregó en Windows 8, para los controladores de administración de conexiones en el grupo de conexiones. Para obtener más información, consulte [Driver-Aware Connection Pooling](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Debe especificar sus propios parámetros de supervisión. Ejemplos de supervisión del rendimiento se han incluido en esta versión de ODBC.
