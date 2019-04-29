---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d0fc510c7c45dab8fbc79cc8e74001ff1855b6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026569"
---
# <a name="compatibility-matrix"></a>Matriz de compatibilidad
En la tabla siguiente describe la compatibilidad de los tipos de aplicaciones y controladores definidos anteriormente en esta sección.  
  
|Tipo de aplicación<br /><br /> y la versión|ODBC de 32 bits<br /><br /> 2.*x* controlador|ODBC 3.*x*<br /><br /> controlador|Controlador de ODBC 3.8|Controlador de ISO y abierto compatible con grupo|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|aplicación de 16 bits, cualquier versión|Compatible|Compatible|Compatible|Compatible|  
|2 puro. *x* aplicación|Compatible|Compatible|Compatible|No compatible con [3]|  
|2 puro. *x* vuelve a compilar la aplicación|Compatible|Compatible [1]|Compatible [1]|No compatible con [3]|  
|2 puro. *x* aplicación Unicode|Compatible|Compatible [1]|Compatible [1]|No compatible con [3]|  
|Aplicación pura Open Group y compatible con ISO|No es compatible|Compatible [2]|Compatible [2]|Compatible [2]|  
|Aplicación 3.0 puro|No es compatible|Compatible|Compatible|No compatible con [4]|  
|Aplicaciones de 3,5 puro|No es compatible|Compatible|Compatible|No compatible con [4]|  
|Aplicación pura de 3,8 (o posterior)|No compatible con [5]|No compatible con [5]|Compatible|No compatible con [4]|  
|Aplicación reemplazado|Compatible|Compatible|Compatible|No compatible con [3]|  
  
 [1] en la aplicación debe volver a compilar mediante los encabezados de ODBC 3.5 (o superiores) con la opción de UNICODE (si se trata de una aplicación de Unicode) y debe establecerse ODBCVER 0x0250.  
  
 [2] en la aplicación debe compilar con encabezados de ODBC 3.5 (o superiores) y vincular con el Administrador de controladores ODBC. También se debe establecer la marca de encabezado ODBC_STD.  
  
 [3] esta configuración potencialmente puede no funcionar porque hay funciones de ODBC 2. *x* que no están en los estándares, como marcadores.  
  
 [4] esta configuración puede producir errores trabajar porque hay características en ODBC 3 *.x* que no están en los estándares, como marcadores.  
  
 [5] esta configuración puede producir errores porque no hay características de ODBC 3.8 que no están en los controladores ODBC de 2.x o 3.x, como específicos del controlador [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Compatibilidad del Administrador de controladores  
 Una aplicación ODBC 3.0 que debe funcionar con todas las versiones del Administrador de controladores debe hacer lo siguiente en el inicio:  
  
-   Asignar un identificador de entorno.  
  
-   Establezca el atributo de entorno de SQL_ATTR_ODBC_VERSION a SQL_OV_ODBC3_80. Si el Administrador de controladores devuelve SQL_ERROR, el Administrador de controladores es anterior a 3.8. Restablecer SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3 o SQL_OV_ODBC2, según corresponda, para que correspondan al administrador de controladores.  
  
-   Asignar un identificador de conexión.  
  
-   Realizar una conexión.  
  
-   Llame a SQLGetInfo para SQL_DRIVER_ODBC_VER determinar la versión del controlador. Si el controlador es un controlador de ODBC 3.8, puede usar los tipos de C específicos del controlador. En caso contrario, no utilice tipos de datos C específicos del controlador.  
  
 Tenga en cuenta que puede usar una aplicación de 3.x ODBC ha vuelto a compilar las funciones de ODBC 3.8 distinto de los tipos de C específicos del controlador sin especificar SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION. Esto es similar a una aplicación de ODBC 2.x ha vuelto a compilar mediante las características ODBC 3.x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Uso de SQLCancelHandle en una aplicación Compatible con todos los administradores de controlador  
 Dado que [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) no se admite en administradores de controlador que se publicaron antes de Windows 7, no se puede cargar una aplicación en versiones anteriores de Windows si llama a **SQLCancelHandle** directamente. Para trabajar con todas las versiones de los administradores de controlador y usar **SQLCancelHandle** en nuevas versiones de Windows, debe llamar una aplicación **SQLCancelHandle** indirectamente mediante el uso de **LoadLibrary** y **GetProcAddress.**  
  
## <a name="see-also"></a>Vea también  
 [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
