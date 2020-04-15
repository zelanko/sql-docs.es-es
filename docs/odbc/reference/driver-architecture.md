---
title: Arquitectura del conductor (Driver Architecture) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ffe2023f028357468700b9bd995d22129ba06817
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294225"
---
# <a name="driver-architecture"></a>Arquitectura de controladores
La arquitectura del controlador se divide en dos categorías, dependiendo del software que procese instrucciones SQL:  
  
-   **Controladores basados en archivos** El controlador accede directamente a los datos físicos. En este caso, el controlador actúa como controlador y origen de datos; es decir, procesa llamadas ODBC e instrucciones SQL. Por ejemplo, los controladores dBASE son controladores basados en archivos porque dBASE no proporciona un motor de base de datos independiente que el controlador puede usar. Es importante tener en cuenta que los desarrolladores de controladores basados en archivos deben escribir sus propios motores de base de datos.  
  
-   **Controladores basados en DBMS** El controlador tiene acceso a los datos físicos a través de un motor de base de datos independiente. En este caso, el controlador procesa solo las llamadas ODBC; pasa instrucciones SQL al motor de base de datos para su procesamiento. Por ejemplo, los controladores de Oracle son controladores basados en DBMS porque Oracle tiene un motor de base de datos independiente que utiliza el controlador. Donde reside el motor de base de datos es irrelevante. Puede residir en la misma máquina que el controlador o una máquina diferente en la red; incluso se puede acceder a través de una puerta de enlace.  
  
 La arquitectura del controlador es generalmente interesante sólo para los escritores de controladores; es decir, la arquitectura del controlador generalmente no hace ninguna diferencia en la aplicación. Sin embargo, la arquitectura puede afectar a si una aplicación puede utilizar SQL específico de DBMS. Por ejemplo, Microsoft Access proporciona un motor de base de datos independiente. Si un controlador de Microsoft Access está basado en DBMS (tiene acceso a los datos a través de este motor) la aplicación puede pasar instrucciones de Microsoft Access-SQL al motor para su procesamiento.  
  
 Sin embargo, si el controlador está basado en archivos , es decir, contiene un motor propietario que tiene acceso directamente al archivo .mdb de Microsoft® Access, es probable que cualquier intento de pasar instrucciones SQL específicas de Microsoft Access al motor dará lugar a errores de sintaxis. La razón es que es probable que el motor propietario implemente solo ODBC SQL.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Controladores basados en archivos](../../odbc/reference/file-based-drivers.md)  
  
-   [Controladores basados en DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Ejemplo de red](../../odbc/reference/network-example.md)  
  
-   [Otras arquitecturas de controlador](../../odbc/reference/other-driver-architectures.md)
