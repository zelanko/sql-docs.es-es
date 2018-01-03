---
title: "Utilizar cadenas de conexión | Documentos de Microsoft"
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
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76aa702a2fe055daaea55f18ffa951f1808e31df
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="using-connection-strings"></a>Utilizar cadenas de conexión
Puede utilizar una cadena de conexión para conectarse a un origen de datos de Visual FoxPro.  
  
 Por ejemplo, para conectarse al origen de datos de TasTrade y de la invalidación de que la configuración actual de exclusivo asociada con el origen de datos, se utilizaría la cadena:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Para obtener una lista de las palabras clave de atributo y los valores que se pueden incluir en la cadena de conexión, consulte [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Para obtener una explicación completa de la sintaxis de la cadena de conexión, consulte [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) en el *referencia del programador de ODBC*.
