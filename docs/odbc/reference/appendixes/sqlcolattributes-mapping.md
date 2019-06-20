---
title: Asignación de SQLColAttributes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7a1508d10431ba9975c44a2002faa4e5b913312
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199410"
---
# <a name="sqlcolattributes-mapping"></a>Asignación de SQLColAttributes
Cuando una aplicación llama **SQLColAttributes** a través de una aplicación ODBC 3 *.x* controlador, la llamada a **SQLColAttributes** se asigna a **SQLColAttribute** como sigue:  
  
> [!NOTE]
>  El prefijo usado en *FieldIdentifier* valores en ODBC 3 *.x* cambió desde que usa en ODBC 2. *x*. El nuevo prefijo es "SQL_DESC"; el prefijo anterior era "SQL_COLUMN".  
  
1.  Si la aplicación es una API ODBC 2. *x* aplicación, *fDescType* es SQL_COLUMN_TYPE, y el tipo devuelto es un tipo DATETIME conciso, el Administrador de controladores se asigna el retorno de los valores de los códigos de fecha, hora y marca de tiempo.  
  
2.  Si *fDescType* es SQL_COLUMN_COUNT, las llamadas del Administrador de controladores, SQL_COLUMN_NULLABLE o SQL_COLUMN_NAME **SQLColAttribute** en el controlador con el *FieldIdentifier* argumento asignado a SQL_DESC_NAME, SQL_DESC_NULLABLE o SQL_DESC_COUNT, según corresponda *.* Todos los demás valores de *fDescType* se pasan al controlador.  
  
 Una aplicación ODBC 3 *.x* controlador debe admitir todos los ODBC 3 *.x* *FieldIdentifiers* enumerados para **SQLColAttribute**.  
  
 Una aplicación ODBC 3 *.x* controlador debe admitir SQL_COLUMN_PRECISION y SQL_DESC_PRECISION, SQL_COLUMN_SCALE y SQL_DESC_SCALE y SQL_COLUMN_LENGTH y SQL_DESC_LENGTH. Estos valores son diferentes porque la precisión, escala y longitud se definen de manera diferente en ODBC 3 *.x* lo que estaban ODBC 2. *x*. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos.
