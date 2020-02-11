---
title: SQLColAttributes (controlador de Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Excel Driver
ms.assetid: 7c4833e3-ff0c-4313-9ab8-21379ceab656
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cd3076ba19b9f5372074a9256e20d73858f69c09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132656"
---
# <a name="sqlcolattributes-excel-driver"></a>SQLColAttributes (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Atributo|Comentarios|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|En el caso de los datos de LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE es la longitud máxima de la columna, no la longitud máxima de los tiempos de la columna 2.|  
|SQL_OWNER_NAME|Se devuelve una cadena vacía ("") en esta columna porque no se admite el nombre del propietario.|  
|SQL_QUALIFIER_NAME|Se devuelve la ruta de acceso a un directorio.|  
|SQL_COLUMN_SEARCHABLE|Las columnas LONGVARBINARY y LONGVARCHAR se muestran como SQL_UNSEARCHABLE.<br /><br /> Los tipos de datos de caracteres y binarios de longitud fija y de longitud variable se pueden buscar, aunque LONGVARBINARY y LONGVARCHAR no lo son.|  
  
> [!NOTE]  
>  Lo anterior no es una lista completa de los atributos devueltos por **SQLColAttributes**.
