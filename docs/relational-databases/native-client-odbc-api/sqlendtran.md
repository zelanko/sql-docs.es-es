---
title: SQLEndTran | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ce7308bd856798869d074c616438945ba845ffa6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32942240"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  De forma predeterminada, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client cierra el cursor asociado de una instrucción cuando **SQLEndTran** confirma o revierte una operación. Los cursores de servidor se cierran, a menos que sean estáticos. Cuando **SQLEndTran** confirma o revierte una operación, el valor del atributo de conexión ODBC específico del controlador SQL_COPT_SS_PRESERVE_CURSORS, establecido por [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), determina el comportamiento del cursor asociado de una instrucción.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de implementación de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [Función SQLEndTran](http://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
