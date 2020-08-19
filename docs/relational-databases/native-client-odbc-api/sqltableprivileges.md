---
description: SQLTablePrivileges
title: SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7be34f8b5ddda112cfb5e16db63256a287c54557
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420729"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SQLTablePrivileges** se puede ejecutar en un cursor estático. Un intento de ejecutar **SQLTablePrivileges** en un control actualizable (controlado por conjunto de claves o dinámico) devuelve SQL_SUCCESS_WITH_INFO que indica que se ha cambiado el tipo de cursor.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el parámetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>Consulte también  
 [SQLTablePrivileges función] (https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [ODBC API Implementation Details](~/relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
