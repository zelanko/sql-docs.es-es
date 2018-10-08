---
title: Método registerOutParameter al tipo y escala | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f80c1fd12f7259820ad094d466bb3f8f132b2c94
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635513"
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
  
 *escala*  
  
 Valor **int** que indica el número de dígitos que se van a colocar a la derecha del signo decimal.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método registerOutParameter especificado por el método registerOutParameter de la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Ver también  
 [Método registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
