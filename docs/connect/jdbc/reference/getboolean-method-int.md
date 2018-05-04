---
title: Método getBoolean (int) | Documentos de Microsoft
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
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBoolean (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d9db847-df22-40ab-8a5c-ec9158c576ca
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4b6c9d23c1d43336a6b83bd634c075705c8c507
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getboolean-method-int"></a>Método getBoolean (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un **booleano** según el índice del parámetro de valor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getBoolean(int index)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 A **booleano** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBoolean es especificado por el método getBoolean en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método getBoolean &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getboolean-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
