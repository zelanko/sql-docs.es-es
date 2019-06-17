---
title: Usar cadenas de conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77bc54f857e04f31ccb982ca40b3ed6334664870
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633210"
---
# <a name="using-connection-strings"></a>Utilizar cadenas de conexión
Puede usar una cadena de conexión para conectarse a un origen de datos de Visual FoxPro.  
  
 Por ejemplo, para conectarse al origen de datos TasTrade e invalidación de que la configuración actual de exclusivo asociada con el origen de datos, usaría la cadena:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Para obtener una lista de las palabras clave de atributo y los valores que se pueden incluir en la cadena de conexión, consulte [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Para obtener una explicación completa de la sintaxis de la cadena de conexión, consulte [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) en el *referencia del programador de ODBC*.
