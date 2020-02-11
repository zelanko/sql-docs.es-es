---
title: SQLTables (dBASE driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLTables
- SQLTables function [ODBC], dBASE Driver
ms.assetid: 45938efb-b678-47d8-9345-644fa26ad679
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 599dbebd8701913b71a482045be121298e39e8c1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132449"
---
# <a name="sqltables-dbase-driver"></a>SQLTables (dBASE controlador)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de dBASE. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El único argumento válido para *szTableOwner* es null porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en null, se devuelven todas las tablas. Se devuelve NULL en el TABLE_OWNER columna.|  
|*szTableQualifier*|En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un directorio.|  
|*SzTableType*|En el caso de los archivos dBASE, "TABLE" es el único tipo de tabla admitido.|
