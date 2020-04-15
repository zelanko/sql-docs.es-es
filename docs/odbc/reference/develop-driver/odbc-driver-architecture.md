---
title: Arquitectura de controladores ODBC (ODBC Driver Architecture) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 712de6a7a3f80ce1cd3ca854a88765dbfa531356
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294563"
---
# <a name="odbc-driver-architecture"></a>Arquitectura de controladores ODBC
Los escritores de controladores deben tener en cuenta que la arquitectura del controlador puede afectar a si una aplicación puede utilizar SQL específico de DBMS.  
  
 ![Muestra la arquitectura del controlador ODBC](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [Controladores basados en archivos](../../../odbc/reference/file-based-drivers.md)  
  
 Cuando el controlador accede a los datos físicos directamente, el controlador actúa como controlador y origen de datos. El controlador debe procesar las llamadas ODBC y las instrucciones SQL. Los desarrolladores de controladores basados en archivos deben escribir sus propios motores de base de datos.  
  
 [Controladores basados en DBMS](../../../odbc/reference/dbms-based-drivers.md)  
  
 Cuando se usa un motor de base de datos independiente para tener acceso a datos físicos, el controlador procesa solo las llamadas ODBC. Pasa instrucciones SQL al motor de base de datos para su procesamiento.  
  
 [Arquitectura de red](../../../odbc/reference/network-example.md)  
  
 Las configuraciones ODBC de archivos y DBMS pueden existir en una sola red.  
  
 [Otras arquitecturas de controlador](../../../odbc/reference/other-driver-architectures.md)  
  
 Cuando se requiere un controlador para trabajar con una variedad de orígenes de datos, se puede utilizar como middleware. La arquitectura heterogénea del motor de unión puede hacer que el controlador aparezca como administrador de controladores. Los controladores también se pueden instalar en servidores, donde pueden ser compartidos por una serie de clientes.  
  
 Para obtener más información acerca de la arquitectura de controladores, vea Administrador de [controladores](../../../odbc/reference/the-driver-manager.md) y arquitectura de [controladores](../../../odbc/reference/driver-architecture.md) en la sección sobre [arquitectura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Puede encontrar más información sobre los problemas del controlador en las ubicaciones descritas en la tabla siguiente.  
  
|Problema|Tema|Location|  
|-----------|-----------|--------------|  
|Problemas de compatibilidad con aplicaciones y controladores|[Compatibilidad de aplicaciones/controladores](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[Consideraciones](../../../odbc/reference/develop-app/programming-considerations.md)de programación , en la referencia del programador ODBC|  
|Escribir controladores ODBC|[Controladores ODBC 3.x de escritura](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[Consideraciones](../../../odbc/reference/develop-app/programming-considerations.md)de programación , en la referencia del programador ODBC|  
|Directrices del controlador para la compatibilidad con versiones anteriores|[Directrices de controlador para la compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[Apéndice G: Directrices del controlador para la compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md), en la referencia del programador ODBC|  
|Conexión a un conductor|[Elegir datos de un origen o el controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[Conexión a un origen](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)de datos o controlador , en la referencia del programador ODBC|  
|Identificación de conductores|[Visualización de controladores](../../../odbc/admin/viewing-drivers.md)|[Visualización de controladores](../../../odbc/admin/viewing-drivers.md), en la Ayuda en línea del Administrador de orígenes de datos ODBC de Microsoft|  
|Habilitación de la agrupación de conexiones|[Agrupación de conexiones ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[Conexión a un origen](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)de datos o controlador , en la referencia del programador ODBC|  
|Problemas de conexión y controlador Unicode/ANSI|[Controladores de Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)|[Consideraciones](../../../odbc/reference/develop-app/programming-considerations.md)de programación , en la referencia del programador ODBC|  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
