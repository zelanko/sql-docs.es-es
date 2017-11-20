---
title: SQLTables (controlador de Excel) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9aad9b74b9813c0526df87437999b66f27e95414
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqltables-excel-driver"></a>SQLTables (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El argumento solo es válido para *szTableOwner* es NULL porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en NULL, se devuelven todas las tablas. Se devuelve NULL en la columna TABLE_OWNER.|  
|*szTableQualifier*|Cuando se usa Microsoft Excel 3.0 o 4.0 del controlador, si se llama a **SQLTables** con un valor para *szTableQualifier* que no es el nombre de una tabla existente, el controlador creará una tabla con ese nombre.<br /><br /> En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un directorio.|  
|*SzTableType*|Para Microsoft Excel 3.0 o 4.0, "TABLE" es el único tipo de tabla admitido.<br /><br /> Las versiones posteriores de los archivos de Microsoft Excel, se devuelve "Tabla del sistema" para los nombres de hoja (tablas con un "$" en el extremo) y se devuelve "TABLE" para las tablas en las hojas de cálculo.|

