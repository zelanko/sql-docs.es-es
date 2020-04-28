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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c436a1f52a862cda753d8c043515f5584607d98c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299305"
---
# <a name="sqltables-excel-driver"></a>SQLTables (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El único argumento válido para *szTableOwner* es null porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en null, se devuelven todas las tablas. Se devuelve NULL en el TABLE_OWNER columna.|  
|*szTableQualifier*|Cuando se usa el controlador Microsoft Excel 3,0 o 4,0, si se llama a **SQLTables** con un valor de *szTableQualifier* que no es el nombre de una tabla existente, el controlador creará una tabla con ese nombre.<br /><br /> En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un directorio.|  
|*SzTableType*|En Microsoft Excel 3,0 o 4,0, "tabla" es el único tipo de tabla admitido.<br /><br /> En las versiones posteriores de los archivos de Microsoft Excel, se devuelve "tabla del sistema" para los nombres de hojas (tablas con un "$" al final) y "TABLE" se devuelve para las tablas de las hojas de cálculo.|
