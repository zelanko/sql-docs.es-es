---
title: Método setInt (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setInt
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7de05cf4-3a48-4c60-9a1b-6ad2ae43d258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45361c22d1e453b12f8bedf2fba2a4c10f02de0d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974186"
---
# <a name="setint-method-sqlservercallablestatement"></a>Método setInt (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el valor **int** indicado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setInt(java.lang.String sCol,  
                   int i)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *i*  
  
 Un valor **int**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setInt especifica este método setInt en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
