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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9083414503606720a40d372ed883a140953dc415
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307596"
---
# <a name="using-connection-strings"></a>Utilizar cadenas de conexión
Puede utilizar una cadena de conexión para conectarse a un origen de datos de Visual FoxPro.  
  
 Por ejemplo, para conectarse al origen de datos TasTrade e invalidar la configuración actual de Exclusive asociada con el origen de datos, usaría la cadena:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Para obtener una lista de las palabras clave y los valores de atributo que puede incluir en la cadena de conexión, consulte [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Para obtener una explicación completa de la sintaxis de la cadena de conexión, vea [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) en la *Referencia del programador de ODBC*.
