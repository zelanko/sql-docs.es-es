---
title: Método registerOutParameter para tipo y escala | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bddc557-4526-4843-9804-05dc83c8832d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb0a97e0b9ee1ef33897d98580a67794fbc8e2bb
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80904281"
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
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *sqlType*  
  
 Un código de tipo JDBC tal como se define en java.sql.Types.  
  
 *scale*  
  
 Valor **int** que indica el número de dígitos que se van a colocar a la derecha del signo decimal.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método registerOutParameter especifica este método registerOutParameter en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
