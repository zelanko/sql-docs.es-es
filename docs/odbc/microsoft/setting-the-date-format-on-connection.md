---
title: "Establecer el formato de fecha en conexión | Documentos de Microsoft"
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
- date formats [ODBC]
- ODBC driver for Oracle [ODBC], date formats
ms.assetid: ba0d5123-db52-448b-8e19-b7647ce4b361
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36011b0a1ea6fbb753c2e091a1e74edce498a31b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-date-format-on-connection"></a>Establecer el formato de fecha en conexión
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 La nueva versión del controlador ODBC de Microsoft para Oracle no establece automáticamente el formato de fecha para los campos de fecha de Oracle. Cuando se conecta el controlador, usaban `ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'`.  
  
 Para establecer el formato de fecha, llamar a ALTER sesión conjunto y, a continuación, realizar la inserción. Por ejemplo:  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```
