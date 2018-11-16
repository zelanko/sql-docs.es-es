---
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c5ab485199920932bd88ce8740a51b7e56152a0b
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51669434"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLTablePrivileges** se puede ejecutar en un cursor estático. Un intento de ejecutar **SQLTablePrivileges** en un cursor actualizable (dinámico o dinámico) devuelve SQL_SUCCESS_WITH_INFO para indicar que el tipo de cursor ha cambiado.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el parámetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLTablePrivileges] (https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [Detalles de implementación de la API de ODBC](~/relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
