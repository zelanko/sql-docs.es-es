---
title: Asignar tipos de datos (controlador ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47646fd6fdf1e8fd16165af1bcfc5e741c6e610f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080738"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Asignar tipos de datos (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El servidor de Oracle admite un conjunto de tipos de datos. El controlador ODBC para Oracle asigna estos tipos de datos a los tipos de datos de ODBC SQL correspondientes. En la tabla siguiente se enumeran los tipos de datos de servidor de Oracle 7,3 y sus tipos de datos de ODBC SQL correspondientes.  
  
 El controlador ODBC para Oracle admite Oracle 7,3 y algunos tipos de datos Oracle8. Para obtener más información sobre los tipos de datos de Oracle8 compatibles, vea [tipos de datos admitidos](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
|Tipo de datos de Oracle Server|Tipo de datos SQL de ODBC|  
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
>  Para obtener más información sobre el tamaño permitido de la columna VARCHAR, vea [tamaño de columna VARCHAR](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) en esta guía.
