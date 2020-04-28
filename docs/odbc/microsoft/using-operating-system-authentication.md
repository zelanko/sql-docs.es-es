---
title: Usar la autenticación de sistema operativo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6520202bdbc31baf1156531457cb70a98656e88
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292845"
---
# <a name="using-operating-system-authentication"></a>Mediante la autenticación de sistema operativo
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 La autenticación del sistema operativo Oracle se basa en el sistema operativo subyacente para controlar el acceso a las cuentas de base de datos. No es necesario que los usuarios escriban una contraseña al usar este tipo de inicio de sesión.  
  
 Para aprovechar esta característica, especifique "/" como identificador de usuario y no especifique una contraseña al conectarse mediante cualquiera de las siguientes API de conexión: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)o [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Las bases de datos de Oracle usan servicios de autenticación de SQL * Net para autenticar a los usuarios que han iniciado sesión. Este servicio funciona bien si los usuarios han iniciado sesión en Oracle a través de SQLPlus; sin embargo, cuando el usuario que ha iniciado sesión es un servicio como Internet Information Services, se produce un error en la autenticación. Se trata de una limitación conocida de\*la autenticación de SQL Net y genera el siguiente error: "[Microsoft] [controlador ODBC para Oracle] [Oracle] ORA-12641: no se pudo inicializar el servicio TNS: autenticación".  
  
 Puede corregir este problema editando el archivo archivo sqlnet. ora. Este archivo de configuración normalmente se almacena en el subdirectorio Network\Admin del directorio principal de Oracle. Agregue la siguiente línea a archivo sqlnet. ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
