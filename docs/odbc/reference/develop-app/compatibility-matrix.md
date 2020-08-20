---
description: Matriz de compatibilidad
title: Matriz de compatibilidad | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bafe3d85e1f4dc1c18acb057fe8c00e4ca0b36d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461571"
---
# <a name="compatibility-matrix"></a>Matriz de compatibilidad
En la tabla siguiente se describe la compatibilidad de los tipos de aplicaciones y controladores definidos anteriormente en esta sección.  
  
|Tipo de aplicación<br /><br /> y versión|ODBC de 32 bits<br /><br /> controlador *2. x*|ODBC *3. x*<br /><br /> controlador|Controlador ODBC 3,8|ISO y abrir controlador compatible con grupos|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|aplicación de 16 bits, cualquier versión|Compatible|Compatible|Compatible|Compatible|  
|Aplicación pura *2. x*|Compatible|Compatible|Compatible|No compatible [3]|  
|Aplicación recompilada pura *2. x*|Compatible|Compatible [1]|Compatible [1]|No compatible [3]|  
|Aplicación Unicode Pure *2. x*|Compatible|Compatible [1]|Compatible [1]|No compatible [3]|  
|Aplicación compatible con ISO y de grupo abierto puro|No compatible|Compatible [2]|Compatible [2]|Compatible [2]|  
|Aplicación pura 3,0|No compatible|Compatible|Compatible|No compatible [4]|  
|Aplicación pura 3,5|No compatible|Compatible|Compatible|No compatible [4]|  
|Aplicación pura 3,8 (o superior)|No compatible [5]|No compatible [5]|Compatible|No compatible [4]|  
|Aplicación reemplazada|Compatible|Compatible|Compatible|No compatible [3]|  
  
 [1] la aplicación debe volver a compilarse con los encabezados ODBC 3,5 (o superior) con la opción Unicode (si es una aplicación Unicode) y debe establecer ODBCVER en 0x0250.  
  
 [2] la aplicación debe compilarse con encabezados ODBC 3,5 (o posterior) y vincularse con el administrador de controladores ODBC. También debe establecer la marca de encabezado ODBC_STD.  
  
 [3] es posible que esta configuración no funcione porque hay características en ODBC *2. x* que no están en los estándares, como los marcadores.  
  
 [4] es posible que esta configuración no funcione porque hay características en ODBC *3. x* que no están en los estándares, como los marcadores.  
  
 [5] puede producirse un error en esta configuración porque hay características en ODBC 3,8 que no están en los controladores ODBC 2. x o 3. x, como los [tipos de datos de C](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)específicos del controlador en ODBC.  
  
## <a name="driver-manager-compatibility"></a>Compatibilidad del administrador de controladores  
 Una aplicación ODBC 3,0 que debe funcionar con todas las versiones del administrador de controladores debe hacer lo siguiente en el inicio:  
  
-   Asigne un identificador de entorno.  
  
-   Establezca el atributo SQL_ATTR_ODBC_VERSION Environment en SQL_OV_ODBC3_80. Si el administrador de controladores devuelve SQL_ERROR, el administrador de controladores es anterior a 3,8. Restablezca SQL_ATTR_ODBC_VERSION a SQL_OV_ODBC3 o SQL_OV_ODBC2, según corresponda, para que se corresponda con el administrador de controladores.  
  
-   Asigne un identificador de conexión.  
  
-   Establecer una conexión.  
  
-   Llame a SQLGetInfo para SQL_DRIVER_ODBC_VER para determinar la versión del controlador. Si el controlador es un controlador ODBC 3,8, puede usar tipos de C específicos del controlador. De lo contrario, no utilice tipos de datos de C específicos del controlador.  
  
 Tenga en cuenta que una aplicación ODBC 3. x recompilada puede usar características de ODBC 3,8 distintas de los tipos de C específicos del controlador sin especificar SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION. Esto es similar a una aplicación ODBC 2. x recompilada que usa las características ODBC 3. x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Usar SQLCancelHandle en una aplicación compatible con todos los administradores de controladores  
 Dado que la [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) no se admite en los administradores de controladores que se publicaron antes de Windows 7, una aplicación no se puede cargar en versiones anteriores de Windows si llama a **SQLCancelHandle** directamente. Para trabajar con todas las versiones de los administradores de controladores y usar **SQLCancelHandle** en nuevas versiones de Windows, una aplicación debe llamar a **SQLCancelHandle** indirectamente mediante **LoadLibrary** y **GetProcAddress.**  
  
## <a name="see-also"></a>Consulte también  
 [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
