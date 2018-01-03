---
title: "Mediante la autenticación de sistema operativo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffcdcf10f0114b9c695031626f707843527050b5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="using-operating-system-authentication"></a>Mediante la autenticación de sistema operativo
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Autenticación de sistema operativo de Oracle se basa en el sistema operativo subyacente para controlar el acceso a las cuentas de base de datos. Los usuarios no necesitan escribir una contraseña cuando se usa este tipo de inicio de sesión.  
  
 Para aprovechar las ventajas de esta característica, especifique "/" como el identificador de usuario y no especifica una contraseña al conectarse a través de cualquiera de la API de conexión siguiente: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md), o [ SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Uso de las bases de datos de Oracle SQL * Net servicios de autenticación para autenticar a los usuarios que han iniciado sesión. Este servicio funciona bien si los usuarios se registran en Oracle a través de SQLPlus; Sin embargo, cuando el usuario ha iniciado la sesión es un servicio, como Internet Information Services, se produce un error en la autenticación. Se trata de una limitación conocida de SQL\*autenticación de red y genera el siguiente error: "[Microsoft] [controlador ODBC para Oracle] [Oracle] ORA-12641: no se pudo inicializar el servicio de TNS:authentication."  
  
 Puede solucionar este problema modificando el archivo Sqlnet.ora. Normalmente, este archivo de configuración se almacena en el subdirectorio Network\Admin del directorio particular de Oracle. Agregue la siguiente línea a Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
