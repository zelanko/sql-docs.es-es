---
title: SQLColAttributes (dBASE controlador) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLColAttributes
ms.assetid: ed44de2b-0b01-4dce-a340-f5eb3aac30b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 56d6a7cb3c2c071191a956c6aaf11479810698f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619623"
---
# <a name="sqlcolattributes-dbase-driver"></a>SQLColAttributes (dBASE controlador)
> [!NOTE]  
>  Este tema proporciona información específica del controlador de dBASE. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Attribute|Comentarios|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Datos LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE es la longitud máxima de la columna, no la longitud máxima de la columna veces 2.|  
|SQL_OWNER_NAME|Una cadena vacía ("") se devuelve en esta columna porque no se admite el nombre del propietario.|  
|SQL_QUALIFIER_NAME|Se devuelve la ruta de acceso a un directorio.|  
|SQL_COLUMN_SEARCHABLE|Columnas LONGVARBINARY y LONGVARCHAR se notifican como SQL_UNSEARCHABLE.<br /><br /> Binario de longitud fija y variable de longitud y tipos de datos de caracteres son para la búsqueda, aunque no sean LONGVARBINARY y LONGVARCHAR.|  
  
> [!NOTE]  
>  El ejemplo anterior no es una lista completa de los atributos devueltos por **SQLColAttributes**.
