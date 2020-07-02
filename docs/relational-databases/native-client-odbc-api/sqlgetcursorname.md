---
title: SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4f91ebce4c21f5b53a467a65e3b1728161ef8996
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789204"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Si la aplicación no especifica un nombre de cursor, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera uno para la aplicación en la generación del cursor. La aplicación puede utilizar **SQLGetCursorName** para recuperar el nombre del cursor definido por controlador para las instrucciones UPDATE y DELETE posicionadas. La aplicación no necesita llamar a **SQLSetCursorName** para sacar provecho de las instrucciones de manipulación de datos posicionadas.  
  
## <a name="see-also"></a>Consulte también  
 [SQLGetCursorName función)](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
