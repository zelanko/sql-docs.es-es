---
title: Matriz de compatibilidad (Compatibility Matrix) Microsoft Docs
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
ms.openlocfilehash: 0406599e1657a900d1669861572ff13834cec670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307458"
---
# <a name="compatibility-matrix"></a>Matriz de compatibilidad
En la tabla siguiente se describe la compatibilidad de los tipos de aplicaciones y controladores definidos anteriormente en esta sección.  
  
|Tipo de aplicación<br /><br /> y versión|ODBC de 32 bits<br /><br /> *Controlador 2.x*|ODBC *3.x*<br /><br /> controlador|Controlador ODBC 3.8|Controlador compatible con ISO y Open Group|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|Aplicación de 16 bits, cualquier versión|Compatible|Compatible|Compatible|Compatible|  
|Aplicación *3.x*|Compatible|Compatible|Compatible|No compatible[3]|  
|Aplicación recompilada *3.x*|Compatible|Compatible[1]|Compatible[1]|No compatible[3]|  
|Aplicación Unicode *3.x* pura|Compatible|Compatible[1]|Compatible[1]|No compatible[3]|  
|Pure Open Group y aplicación compatible con ISO|No compatible|Compatible[2]|Compatible[2]|Compatible[2]|  
|Aplicación 3.0 pura|No compatible|Compatible|Compatible|No compatible[4]|  
|Aplicación pura 3.5|No compatible|Compatible|Compatible|No compatible[4]|  
|Aplicación pura 3.8 (o superior)|No compatible [5]|No compatible [5]|Compatible|No compatible [4]|  
|Aplicación reemplazada|Compatible|Compatible|Compatible|No compatible[3]|  
  
 [1] La aplicación debe volver a compilar mediante encabezados ODBC 3.5 (o superior) con la opción UNICODE (si es una aplicación Unicode) y debe establecer ODBCVER en 0x0250.  
  
 [2] La aplicación debe compilar mediante ENCABEZADOs ODBC 3.5 (o superior) y vincular con el Administrador de controladores ODBC. También debe establecer el indicador de encabezado ODBC_STD.  
  
 [3] Esta configuración puede potencialmente no funcionar porque hay características en ODBC *2.x* que no están en los estándares, como marcadores.  
  
 [4] Esta configuración puede potencialmente no funcionar porque hay características en ODBC *3.x* que no están en los estándares, como marcadores.  
  
 [5] Esta configuración puede producir un error posible porque hay características en ODBC 3.8 que no están en controladores ODBC 2.x o 3.x, como tipos de datos C específicos del controlador [en ODBC.](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)  
  
## <a name="driver-manager-compatibility"></a>Compatibilidad con Driver Manager  
 Una aplicación ODBC 3.0 que debe funcionar con todas las versiones del Administrador de controladores debe hacer lo siguiente al iniciar:  
  
-   Asigne un identificador de entorno.  
  
-   Establezca el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3_80. Si el Administrador de controladores devuelve SQL_ERROR, el Administrador de controladores es anterior a 3.8. Restablezca SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC3 o SQL_OV_ODBC2, según corresponda, para que correspondan al Administrador de controladores.  
  
-   Asigne un identificador de conexión.  
  
-   Haz una conexión.  
  
-   Llame a SQLGetInfo para SQL_DRIVER_ODBC_VER para determinar la versión del controlador. Si el controlador es un controlador ODBC 3.8, puede usar tipos de C específicos del controlador. De lo contrario, no utilice tipos de datos C específicos del controlador.  
  
 Tenga en cuenta que una aplicación ODBC 3.x recompilada puede usar características ODBC 3.8 distintas de los tipos de C específicos del controlador sin especificar SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION. Esto es similar a una aplicación ODBC 2.x recompilada mediante características ODBC 3.x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Uso de SQLCancelHandle en una aplicación compatible con todos los administradores de controladores  
 Dado que [SQLCancelHandle (función)](../../../odbc/reference/syntax/sqlcancelhandle-function.md) no se admite en los administradores de controladores que se publicaron antes de Windows 7, no se puede cargar una aplicación en versiones anteriores de Windows si llama a **SQLCancelHandle** directamente. Para trabajar con todas las versiones de administradores de controladores y usar **SQLCancelHandle** en nuevas versiones de Windows, una aplicación debe llamar a **SQLCancelHandle** indirectamente mediante **LoadLibrary** y **GetProcAddress.**  
  
## <a name="see-also"></a>Consulte también  
 [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
