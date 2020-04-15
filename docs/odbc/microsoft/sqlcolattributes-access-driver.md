---
title: SQLColAttributes (controlador de acceso) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15770ac260ad8ea864dc78bf00c5b9e8bd964dbe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307966"
---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Atributo|Comentarios|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Para los datos LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE es la longitud máxima de la columna, no la longitud máxima de la columna por 2.|  
|SQL_OWNER_NAME|Se devuelve una cadena vacía ("") en esta columna porque no se admite el nombre del propietario.|  
|SQL_QUALIFIER_NAME|Se devuelve la ruta de acceso a un archivo de base de datos.|  
|SQL_COLUMN_SEARCHABLE|Las columnas LONGVARBINARY y LONGVARCHAR se notifican como SQL_UNSEARCHABLE.<br /><br /> Los tipos de datos binarios y de caracteres de longitud fija y de longitud variable se pueden buscar, aunque LONGVARBINARY y LONGVARCHAR no lo sean.|  
  
> [!NOTE]  
>  Lo anterior no es una lista completa de los atributos devueltos por **SQLColAttributes**.
