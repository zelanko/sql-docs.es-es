---
title: "Método registerOutParameter al tipo y escala | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.registerOutParameter (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bddc557-4526-4843-9804-05dc83c8832d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 341300744a1a3643e6ac0cbbcb22d36c573de32b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="registeroutparameter-method-javalangstring-int-int"></a>Método registerOutParameter (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra el parámetro OUT con el nombre especificado para el tipo JDBC y la escala determinados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void registerOutParameter(java.lang.String s,  
                                 int n,  
                                 int n1)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *s*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *sqlType*  
  
 Un código de tipo JDBC tal como se define en java.sql.Types.  
  
 *escala*  
  
 Un **int** que indica el número de dígitos que se va a colocar a la derecha del separador decimal.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método registerOutParameter especificado por el método registerOutParameter de la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método registerOutParameter &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

