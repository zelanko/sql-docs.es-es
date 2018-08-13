---
title: SQLFreeHandle | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fe6e241e1596fd81cfc4cc284088a1ceacc6cfd7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559085"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  En el modo de confirmación manual, al llamar a **SQLFreeHandle** en un identificador de instrucción con una transacción abierta se produce una operación de reversión de cambios pendientes a la base de datos. Al llamando a **SQLFreeHandle** en un identificador de instrucción siempre se cierra cualquier cursor abierto y se descartan los resultados pendientes, liberando todos los recursos asociados con el identificador de instrucción.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLFreeHandle](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
