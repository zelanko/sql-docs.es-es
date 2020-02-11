---
title: SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8e3cee37a124c40c21e6d8ee8829dcf7f39e808
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73786831"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite las actualizaciones y eliminaciones en cascada a través del mecanismo de restricciones de clave externa. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve SQL_CASCADE para las columnas UPDATE_RULE o DELETE_RULE si se ha especificado la opción CASCADE en las cláusulas ON UPDATE u ON DELETE de las restricciones FOREIGN KEY. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve SQL_NO_ACTION para las columnas UPDATE_RULE o DELETE_RULE si se ha especificado la opción NO ACTION en las cláusulas ON UPDATE u ON DELETE de las restricciones FOREIGN KEY.  
  
 Cuando los valores no válidos están presentes en cualquier parámetro **SQLForeignKeys** , **SQLForeignKeys** devuelve SQL_SUCCESS en ejecución. **SQLFetch** devuelve SQL_NO_DATA cuando se usan valores no válidos en estos parámetros.  
  
 **SQLForeignKeys** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLForeignKeys** en un cursor actualizable (dinámico o Keyset) devuelve SQL_SUCCESS_WITH_INFO que indica que se ha cambiado el tipo de cursor.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite la información de informes de tablas en servidores vinculados aceptando un nombre de dos partes para los parámetros *FKCatalogName* y *PKCatalogName* : *Linked_Server_Name. Catalog_Name*.  
  
## <a name="see-also"></a>Consulte también  
 [SQLForeignKeys función)](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
