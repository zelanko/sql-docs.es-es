---
description: SQLColAttributes (controlador de Access)
title: SQLColAttributes (controlador de Access) | Microsoft Docs
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
ms.openlocfilehash: d9758bb5c473971d3ed9acea52559da0a4aac67d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412281"
---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Atributo|Comentarios|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|En el caso de los datos de LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE es la longitud máxima de la columna, no la longitud máxima de los tiempos de la columna 2.|  
|SQL_OWNER_NAME|Se devuelve una cadena vacía ("") en esta columna porque no se admite el nombre del propietario.|  
|SQL_QUALIFIER_NAME|Se devuelve la ruta de acceso a un archivo de base de datos.|  
|SQL_COLUMN_SEARCHABLE|Las columnas LONGVARBINARY y LONGVARCHAR se muestran como SQL_UNSEARCHABLE.<br /><br /> Los tipos de datos de caracteres y binarios de longitud fija y de longitud variable se pueden buscar, aunque LONGVARBINARY y LONGVARCHAR no lo son.|  
  
> [!NOTE]  
>  Lo anterior no es una lista completa de los atributos devueltos por **SQLColAttributes**.
