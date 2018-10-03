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
manager: craigg
ms.openlocfilehash: 9931d3d02ff2d0afe69f410d94474c16f235b94e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695023"
---
# <a name="sqltables-access-driver"></a>SQLTables (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El argumento solo es válido para *szTableOwner* es NULL porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en NULL, se devuelven todas las tablas. Se devuelve NULL en la columna TABLE_OWNER.|  
|*szTableQualifier*|En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un archivo de base de datos.|  
|*SzTableType*|Cuando se usa el controlador de Microsoft Access, se admite la "Tabla del sistema" para *szTableType* para las tablas del sistema, se admite "Sinónimo" de las tablas asociadas, y es compatible con "VIEW" devuelve filas las consultas.|  
  
## <a name="see-also"></a>Vea también  
 [Función SQLTables](../../odbc/reference/syntax/sqltables-function.md)
