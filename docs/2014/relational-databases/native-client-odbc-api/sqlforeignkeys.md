---
title: SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: rothja
ms.author: jroth
ms.openlocfilehash: a61e80867abb8ecb4d2628b74dc9956051c8e4ce
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022385"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite las actualizaciones y eliminaciones en cascada a través del mecanismo de restricciones de clave externa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve SQL_CASCADE para las columnas UPDATE_RULE o DELETE_RULE si se ha especificado la opción CASCADE en las cláusulas ON UPDATE u ON DELETE de las restricciones FOREIGN KEY. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve SQL_NO_ACTION para las columnas UPDATE_RULE o DELETE_RULE si se ha especificado la opción NO ACTION en las cláusulas ON UPDATE u ON DELETE de las restricciones FOREIGN KEY.  
  
 Cuando los valores no válidos están presentes en cualquier parámetro **SQLForeignKeys** , **SQLForeignKeys** devuelve SQL_SUCCESS en ejecución. **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
 **SQLForeignKeys** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLForeignKeys** en un cursor actualizable (dinámico o Keyset) devuelve SQL_SUCCESS_WITH_INFO que indica que se ha cambiado el tipo de cursor.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite la información de informes de tablas en servidores vinculados aceptando un nombre de dos partes para los parámetros *FKCatalogName* y *PKCatalogName* : *Linked_Server_Name. Catalog_Name*.  
  
## <a name="see-also"></a>Consulte también  
 [SQLForeignKeys función)](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
