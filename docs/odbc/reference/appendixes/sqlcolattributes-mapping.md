---
title: Asignación de SQLColAttributes (SQLColAttributes Mapping) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c2c8386d6771141eaa0145a5d5964d70d6084d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305421"
---
# <a name="sqlcolattributes-mapping"></a>Asignación de SQLColAttributes
Cuando una aplicación llama a **SQLColAttributes** a través de un controlador ODBC *3.x,* la llamada a **SQLColAttributes** se asigna a **SQLColAttribute de** la siguiente manera:  
  
> [!NOTE]
>  El prefijo utilizado en los valores *FieldIdentifier* en ODBC *3.x* se ha cambiado del utilizado en ODBC *2.x*. El nuevo prefijo es "SQL_DESC"; el prefijo antiguo era "SQL_COLUMN".  
  
1.  Si la aplicación es una aplicación ODBC *2.x,* *fDescType* es SQL_COLUMN_TYPE y el tipo devuelto es un tipo DATETIME conciso, el Administrador de controladores asigna los valores devueltos para los códigos de fecha, hora y marca de tiempo.  
  
2.  Si *fDescType* está SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE o SQL_COLUMN_COUNT, el Administrador de controladores llama a **SQLColAttribute** en el controlador con el Argumento *FieldIdentifier* asignado a SQL_DESC_NAME, SQL_DESC_NULLABLE o SQL_DESC_COUNT, según*corresponda.* Todos los demás valores de *fDescType* se pasan al controlador.  
  
 Un controlador ODBC *3.x* debe admitir todos los *identificadores de campo* ODBC *3.x* enumerados para **SQLColAttribute**.  
  
 Un controlador ODBC *3.x* debe admitir SQL_COLUMN_PRECISION y SQL_DESC_PRECISION, SQL_COLUMN_SCALE y SQL_DESC_SCALE, y SQL_COLUMN_LENGTH y SQL_DESC_LENGTH. Estos valores son diferentes porque la precisión, la escala y la longitud se definen de forma diferente en ODBC *3.x* que en ODBC *2.x*. Para obtener más información, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en Apéndice D: Tipos de datos.
