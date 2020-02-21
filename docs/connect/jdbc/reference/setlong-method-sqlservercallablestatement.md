---
title: Método setLong (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setLong
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 137416fe-a580-424e-be79-fe946eba9e6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f7110594eb808a50fa88e22b1e38d2a4052066f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974039"
---
# <a name="setlong-method-sqlservercallablestatement"></a>Método setLong (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el valor **long** indicado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setLong(java.lang.String sCol,  
                    long l)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *l*  
  
 Un valor **long**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setLong especifica este método setLong en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
