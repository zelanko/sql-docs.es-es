---
title: SQLTables (controlador de Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23ce67350b7fa7d0a88f3d51e618ce9bb9f9ebcf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796223"
---
# <a name="sqltables-excel-driver"></a>SQLTables (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El argumento solo es válido para *szTableOwner* es NULL porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en NULL, se devuelven todas las tablas. Se devuelve NULL en la columna TABLE_OWNER.|  
|*szTableQualifier*|Cuando se usa Microsoft Excel 3.0 o 4.0 del controlador, si se llama a **SQLTables** con un valor para *szTableQualifier* que no es el nombre de una tabla existente, el controlador creará una tabla con ese nombre.<br /><br /> En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un directorio.|  
|*SzTableType*|Para Microsoft Excel 3.0 o 4.0, "TABLE" es el único tipo de tabla admitido.<br /><br /> Para las versiones posteriores de los archivos de Microsoft Excel, se devuelve "Tabla del sistema" para los nombres de hoja (tablas con un carácter "$" en el extremo) y se devuelve "TABLE" para las tablas en las hojas de cálculo.|
