---
title: SQLColAttributes (dBASE driver) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9e9d5adb75a99784d7244852bfda0499e481fc4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307956"
---
# <a name="sqlcolattributes-dbase-driver"></a>SQLColAttributes (dBASE controlador)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de dBASE. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Atributo|Comentarios|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|En el caso de los datos de LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE es la longitud máxima de la columna, no la longitud máxima de los tiempos de la columna 2.|  
|SQL_OWNER_NAME|Se devuelve una cadena vacía ("") en esta columna porque no se admite el nombre del propietario.|  
|SQL_QUALIFIER_NAME|Se devuelve la ruta de acceso a un directorio.|  
|SQL_COLUMN_SEARCHABLE|Las columnas LONGVARBINARY y LONGVARCHAR se muestran como SQL_UNSEARCHABLE.<br /><br /> Los tipos de datos de caracteres y binarios de longitud fija y de longitud variable se pueden buscar, aunque LONGVARBINARY y LONGVARCHAR no lo son.|  
  
> [!NOTE]  
>  Lo anterior no es una lista completa de los atributos devueltos por **SQLColAttributes**.
