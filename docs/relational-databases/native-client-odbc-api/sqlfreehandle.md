---
title: SQLFreeHandle ? Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc8a8cac364c9226d32ed2ebadbc2702e13031ab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298462"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En el modo de confirmación manual, al llamar a **SQLFreeHandle** en un identificador de instrucción con una transacción abierta se produce una operación de reversión de cambios pendientes a la base de datos. Al llamando a **SQLFreeHandle** en un identificador de instrucción siempre se cierra cualquier cursor abierto y se descartan los resultados pendientes, liberando todos los recursos asociados con el identificador de instrucción.  
  
## <a name="see-also"></a>Consulte también  
 [Función SQLFreeHandle](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
