---
title: Asignar tipos de datos (controlador ODBC para Oracle) | Documentos de Microsoft
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
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6384f81f03a20e46a1d2a6434063caf32577554
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Asignar tipos de datos (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El servidor de Oracle admite un conjunto de tipos de datos. El controlador ODBC para Oracle asigna estos tipos de datos a sus tipos de datos SQL de ODBC adecuados. En la tabla siguiente se enumera los tipos de datos de Oracle 7.3 Server y sus tipos de datos de ODBC SQL correspondientes.  
  
 El controlador ODBC para Oracle admite Oracle 7.3 y algunos tipos de datos de Oracle8. Para obtener más información acerca de los tipos de datos de Oracle8 compatibles, consulte [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
|Tipo de datos del servidor de Oracle|Tipo de datos SQL de ODBC|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|DATE|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  Para obtener más información sobre el tamaño permitido de la columna VARCHAR, consulte [tamaño de la columna VARCHAR](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) en esta guía.

