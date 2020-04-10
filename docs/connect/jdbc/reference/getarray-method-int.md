---
title: Método getArray (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getArray (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5b839d3f-5a4e-43da-b93c-dc9e0f6d4b3b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d1c6e2f5cac93ab188ecae0f798722541b62e69
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923445"
---
# <a name="getarray-method-int"></a>Método getArray (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto Array según el índice de parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Array getArray(int i)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *i*  
  
 Un valor **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Array.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getArray especifica este método getArray en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método getArray &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
