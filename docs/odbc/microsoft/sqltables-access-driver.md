---
title: SQLTables (controlador de Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e23e6993f66dd706a800ae2b34a9fdc0d219898d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132461"
---
# <a name="sqltables-access-driver"></a>SQLTables (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El único argumento válido para *szTableOwner* es null porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en null, se devuelven todas las tablas. Se devuelve NULL en el TABLE_OWNER columna.|  
|*szTableQualifier*|En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un archivo de base de datos.|  
|*SzTableType*|Cuando se usa el controlador de Microsoft Access, se admite "tabla del sistema" para *szTableType* en las tablas del sistema, "SYNONYM" es compatible con las tablas adjuntas y "View" se admite para las consultas que devuelven filas.|  
  
## <a name="see-also"></a>Consulte también  
 [Función SQLTables](../../odbc/reference/syntax/sqltables-function.md)
