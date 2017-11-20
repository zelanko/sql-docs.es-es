---
title: 'SQL en C: GUID | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0d60ca76d44f443c564bd354535833ab6c7b407f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-guid"></a>SQL en el GUID de C:
El identificador para el tipo de datos SQL de ODBC de GUID es:  
  
 SQL_GUID  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos de SQL de GUID de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres|data|36|n/d|  
||*BufferLength* < 37|No definido|No definido|22003|  
|SQL_C_WCHAR|*BufferLength* > longitud de caracteres|data|36|n/d|  
||*BufferLength* < 37|No definido|No definido|22003|  
|SQL_C_BINARY|Longitud de bytes de datos \< =  *BufferLength*|data|Longitud de los datos en bytes|n/d|  
||Longitud de bytes de datos > *BufferLength*|No definido|No definido|22003|  
|SQL_C_GUID|Ninguno [a]|data|16 [b]|n/d|  
  
 [a] el valor de *BufferLength* se pasa por alto para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] es el tamaño del tipo de datos C correspondiente.

