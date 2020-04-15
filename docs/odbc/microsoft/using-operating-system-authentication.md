---
title: Uso de la autenticación del sistema operativo (Operating System Authentication) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292845"
---
# <a name="using-operating-system-authentication"></a>Mediante la autenticación de sistema operativo
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 La autenticación del sistema operativo Oracle se basa en el sistema operativo subyacente para controlar el acceso a las cuentas de base de datos. Los usuarios no necesitan introducir una contraseña al utilizar este tipo de inicio de sesión.  
  
 Para aprovechar esta característica, especifique "/" como ID de usuario y no especifique una contraseña al conectarse mediante cualquiera de las siguientes API de conexión: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)o [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Las bases de datos de Oracle utilizan SQL*Net Authentication Services para autenticar a los usuarios que han iniciado sesión. Este servicio funciona bien si los usuarios inician sesión en Oracle a través de SQLPlus; sin embargo, cuando el usuario que ha iniciado sesión es un servicio como Internet Information Services, se produce un error en la autenticación. Esta es una limitación conocida de la autenticación de red\*sql y produce el siguiente error: "[Microsoft][controlador ODBC para Oracle][Oracle]ORA-12641: TNS:authentication service failed to initialize."  
  
 Puede corregir este problema editando el archivo Sqlnet.ora. Este archivo de configuración se suele almacenar en el subdirectorio Network-Admin del directorio principal de Oracle. Agregue la siguiente línea a Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
