---
title: Método getMaxIndexLength (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxIndexLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c85d021-d466-4732-85f9-53903d297041
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eff5203b666a0593a27f6484b6318ef852d2ce8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906929"
---
# <a name="getmaxindexlength-method-sqlserverdatabasemetadata"></a>Método getMaxIndexLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de bytes que esta base de datos permite para un índice, lo cual incluye todas las partes del índice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getMaxIndexLength()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el número máximo permitido de bytes.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getMaxIndexLength especifica este método getMaxIndexLength en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
