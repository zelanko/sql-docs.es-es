---
title: SQLCancel | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: abd731f199e04acb098e8709a7c09dacc7ba27e9
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39541505"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El tema [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516) establece que en ODBC 2.x, si una aplicación llama a **SQLCancel** cuando no se está realizando ningún procesamiento en la instrucción, **SQLCancel** tiene el mismo efecto que **SQLFreeStmt** con la opción **SQL_CLOSE** ; este compotamiento se define solamente po razones de compleción y las aplicaciones deben llamar a **SQLFreeStmt** o **SQLCloseCurso** to close cursos. Pero aunque la aplicación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establezca que la versión de la API de ODBC ha de ser 3.5.x o posterior, la función **SQLCancel** utilizará el comportamiento de ODBC 2.x.  
  
## <a name="see-also"></a>Vea también  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
