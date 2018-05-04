---
title: Asignación de SQLColAttributes | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 615ee316c8fe515ebbd3d983cd32e70bbcb8681e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcolattributes-mapping"></a>Asignación de SQLColAttributes
Cuando una aplicación llama **SQLColAttributes** a través de una aplicación ODBC 3 *.x* controlador, la llamada a **SQLColAttributes** se asigna a **SQLColAttribute** como se indica a continuación:  
  
> [!NOTE]  
>  El prefijo usado en *FieldIdentifier* valores en ODBC 3 *.x* cambió desde que usa en ODBC 2. *x*. El nuevo prefijo es "SQL_DESC"; el prefijo anterior era "SQL_COLUMN".  
  
1.  Si la aplicación es una API ODBC 2. *x* aplicación, *fDescType* es SQL_COLUMN_TYPE, y el tipo de valor devuelto es un tipo de fecha y hora conciso, las asignaciones de administrador de controladores, la devolución de valores para los códigos de fecha, hora y marca de tiempo.  
  
2.  Si *fDescType* es SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE o SQL_COLUMN_COUNT, las llamadas de administrador de controladores **SQLColAttribute** en el controlador con el *FieldIdentifier* argumento asignado a SQL_DESC_NAME, SQL_DESC_NULLABLE o SQL_DESC_COUNT, según corresponda *.* Todos los demás valores de *fDescType* se pasan al controlador.  
  
 Una aplicación ODBC 3 *.x* controlador debe admitir el 3 de ODBC *.x* *FieldIdentifiers* enumerados para **SQLColAttribute**.  
  
 Una aplicación ODBC 3 *.x* controlador debe admitir SQL_COLUMN_PRECISION y SQL_DESC_PRECISION, SQL_COLUMN_SCALE y SQL_DESC_SCALE y SQL_COLUMN_LENGTH y SQL_DESC_LENGTH. Estos valores son diferentes porque precisión, escala y longitud se definen de manera diferente en ODBC 3 *.x* que estuvieran en ODBC 2. *x*. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en tipos de datos de apéndice D:.
