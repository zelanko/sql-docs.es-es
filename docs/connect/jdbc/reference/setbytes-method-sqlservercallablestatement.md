---
title: Método setBytes (SQLServerCallableStatement) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerCallableStatement.setBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f264f1a6-ee35-4eaf-81d8-ecf99f03b35d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea7c949ae8bfa36e276ce05cd1f32d7d39f00431
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="setbytes-method-sqlservercallablestatement"></a>Método setBytes (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en la matriz indicada de **bytes** valores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setBytes(java.lang.String sCol,  
                     byte[] b)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *B*  
  
 Una matriz de **bytes** valores.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 En una versión anterior del controlador, se podía utilizar SQLServerCallableStatement.setBytes para convertir valores entre las matrices de bytes y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de datos **fecha**, **tiempo**, **datetime2** , o **datetimeoffset**. Ahora, al usar este método con esos tipos de datos, se producirá una excepción que indica que no se admite la conversión.  
  
 Este método setBytes es especificado por el método setBytes en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
