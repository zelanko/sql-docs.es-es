---
title: SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f2c4851b4cbb88c0d927aa4739e06501ce5ca1b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298515"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  De forma predeterminada, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client cierra el cursor asociado de una instrucción cuando **SQLEndTran** confirma o revierte una operación. Los cursores de servidor se cierran, a menos que sean estáticos. Cuando **SQLEndTran** confirma o revierte una operación, el valor del atributo de conexión ODBC específico del controlador SQL_COPT_SS_PRESERVE_CURSORS, establecido por [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), determina el comportamiento del cursor asociado de una instrucción.  
  
## <a name="see-also"></a>Consulte también  
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [Función SQLEndTran](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
