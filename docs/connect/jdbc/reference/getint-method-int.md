---
title: Método getInt (int) | Documentos de Microsoft
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
- SQLServerCallableStatement.getInt (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c86792bb-096e-4c58-8b9e-74491ccf83a6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e595d8364ce99a5f4225346b14ac5d29139fa21a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getint-method-int"></a>Método getInt (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un **int** en el lenguaje según el índice de parámetro de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getInt(int index)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getInt especificado por el método getInt en la interfaz java.sql.CallableStatement.  
  
 Este método solo se admite en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de datos que pueden devolver un valor entero como int, smallint, tinyint y bit de forma segura. Si se utiliza este método en cualquier otro tipo de datos, provocará una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Método getInt &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
