---
title: Admite los tipos de datos (controlador ODBC para Oracle) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f6e80b887659679992091a32faf2763d71d9f6f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>Tipos de datos admitidos (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC para Oracle admite todos los tipos de datos de Oracle 7.3; Sin embargo, no admite cualquiera de los nuevos tipos de datos de Oracle8 enumerados aquí.  
  
|Tipo de datos|Oracle 7.3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/d|No compatible|  
|BLOB|n/d|No compatible|  
|CHAR|Compatible|Compatible|  
|CLOB|n/d|No compatible|  
|DATE|Compatible|Compatible|  
|FLOAT|Compatible|Compatible|  
|INTEGER|Compatible|Compatible|  
|LONG|Compatible|Compatible|  
|LONG RAW|Compatible|Compatible|  
|NCHAR|n/d|No compatible|  
|NCLOB|n/d|No compatible|  
|NUMBER|Compatible|Compatible|  
|NVARCHAR2|n/d|No compatible|  
|RAW|Compatible|Compatible|  
|VARCHAR2|Compatible|Compatible|  
|MLSLABEL|No compatible.|No compatible.|  
  
> [!NOTE]  
>  Para obtener más información sobre el tamaño permitido de la columna VARCHAR, consulte [tamaño de la columna VARCHAR](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) en esta guía.
