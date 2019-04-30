---
title: Mediante la autenticación de sistema operativo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a532c253ea2204fa3636c24c503cbefd3fa6311
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127812"
---
# <a name="using-operating-system-authentication"></a>Mediante la autenticación de sistema operativo
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Autenticación de sistema operativo de Oracle se basa en el sistema operativo subyacente para controlar el acceso a las cuentas de base de datos. Los usuarios no necesitan escribir una contraseña cuando se usa este tipo de inicio de sesión.  
  
 Para aprovechar las ventajas de esta característica, especifique "/" como el identificador de usuario y no se especifica una contraseña al conectarse usando cualquiera de la API de conexión siguiente: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md), o [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Uso de las bases de datos de Oracle SQL * Net servicios de autenticación para autenticar a los usuarios que han iniciado sesión. Este servicio funciona bien si los usuarios se registran en Oracle a través de SQLPlus; Sin embargo, cuando el usuario ha iniciado sesión es un servicio, como Internet Information Services, se produce un error en la autenticación. Se trata de una limitación conocida de SQL\*autenticación de red y genera el siguiente error: "[Microsoft] [controlador ODBC para Oracle] [Oracle] ORA-12641: Servicio TNS:Authentication no se pudo inicializar."  
  
 Puede solucionar este problema, edite el archivo Sqlnet.ora. Normalmente, este archivo de configuración se almacena en el subdirectorio Network\Admin del directorio principal de Oracle. Agregue la siguiente línea a Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
