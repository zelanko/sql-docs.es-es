---
title: Arquitectura del controlador | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a74f6e1b212f570ba9aa47a09310b63b13ee0e42
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="driver-architecture"></a>Arquitectura de controladores
Arquitectura de controladores se divide en dos categorías, dependiendo de los procesos de software instrucciones SQL:  
  
-   **Controladores basados en archivos** el controlador tiene acceso directo a los datos físicos. En este caso, el controlador actúa como controlador y el origen de datos; es decir, procesa las llamadas ODBC e instrucciones SQL. Por ejemplo, controladores de dBASE son controladores basados en archivos porque dBASE no proporciona que un motor de base de datos independiente del controlador puede usar. Es importante tener en cuenta que los desarrolladores de controladores basados en archivos deben escribir sus propios motores de base de datos.  
  
-   **Controladores basados en DBMS** el controlador tiene acceso a los datos físicos a través de un motor de base de datos independiente. En este caso, el controlador procesa solo las llamadas ODBC; pasa instrucciones SQL al motor de base de datos para su procesamiento. Por ejemplo, controladores de Oracle son controladores basados en DBMS porque Oracle tiene un motor de base de datos independiente que usa el controlador. En el que reside el motor de base de datos es irrelevante. Puede residir en el mismo equipo que el controlador o un equipo diferente de la red; incluso puede obtenerse a través de una puerta de enlace.  
  
 Arquitectura del controlador es interesante generalmente solo para los escritores de controladores; es decir, arquitectura de controlador generalmente produce ninguna diferencia a la aplicación. Sin embargo, la arquitectura puede afectar a si una aplicación puede utilizar SQL específicos de DBMS. Por ejemplo, Microsoft Access proporciona un motor de base de datos independiente. Si un controlador de Microsoft Access se basa en el DBMS: tener acceso a los datos a través de este motor, la aplicación puede pasar las instrucciones SQL de Microsoft Access para el motor para su procesamiento.  
  
 Sin embargo, si el controlador se basa en el archivo, es decir, contiene un motor propietario que accede directamente el archivo .mdb de Microsoft® Access, cualquier intento de pasar instrucciones SQL específicas de Microsoft Access al motor suelen dar lugar a errores de sintaxis. La razón es que el motor de propiedad es probable que implementar solo ODBC SQL.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Controladores basados en archivos](../../odbc/reference/file-based-drivers.md)  
  
-   [Controladores basados en DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Ejemplo de red](../../odbc/reference/network-example.md)  
  
-   [Otras arquitecturas de controlador](../../odbc/reference/other-driver-architectures.md)

