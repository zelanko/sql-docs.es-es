---
title: Admite los tipos de datos (controlador ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 219a6d2e837280ca3220382bea56d2ab610ce87a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270886"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>Tipos de datos admitidos (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC para Oracle es compatible con todos los tipos de datos de Oracle 7.3; Sin embargo, no admite cualquiera de los nuevos tipos de datos de Oracle8 enumerados aquí.  
  
|Tipo de datos|Oracle 7.3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/d|No compatible|  
|BLOB|n/d|No compatible|  
|CHAR|Admitida|Admitida|  
|CLOB|n/d|No compatible|  
|DATE|Admitida|Admitida|  
|FLOAT|Admitida|Admitida|  
|INTEGER|Admitida|Admitida|  
|LONG|Admitida|Admitida|  
|LONG RAW|Admitida|Admitida|  
|NCHAR|n/d|No compatible|  
|NCLOB|n/d|No compatible|  
|NUMBER|Admitida|Admitida|  
|NVARCHAR2|n/d|No compatible|  
|RAW|Admitida|Admitida|  
|VARCHAR2|Admitida|Admitida|  
|MLSLABEL|No compatible.|No compatible.|  
  
> [!NOTE]  
>  Para obtener más información sobre el tamaño permitido de la columna VARCHAR, consulte [tamaño de la columna VARCHAR](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) en esta guía.
