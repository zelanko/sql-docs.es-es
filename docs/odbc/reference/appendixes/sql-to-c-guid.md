---
title: 'SQL a C: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f0f247bc4cb411d535050d7c78e0ea42cc144b0e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296465"
---
# <a name="sql-to-c-guid"></a>SQL a C: GUID
El identificador para el tipo de datos SQL de ODBC de GUID es:  
  
 SQL_GUID  
  
 En la tabla siguiente se muestran los tipos de datos de ODBC C en los que se pueden convertir los datos de SQL de GUID. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos de C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres|data|36|N/D|  
||*BufferLength* < 37|No definido|No definido|22003|  
|SQL_C_WCHAR|*BufferLength* longitud de caracteres de >|data|36|N/D|  
||*BufferLength* < 37|No definido|No definido|22003|  
|SQL_C_BINARY|Longitud de bytes \< = de *BufferLength* de datos|data|Longitud de los datos en bytes|N/D|  
||Longitud de bytes de los datos > *BufferLength*|No definido|No definido|22003|  
|SQL_C_GUID|Ninguno [a]|data|16 [b]|N/D|  
  
 [a] el valor de *BufferLength* se omite para esta conversión. El controlador supone que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos de C.  
  
 [b] es el tamaño del tipo de datos de C correspondiente.
