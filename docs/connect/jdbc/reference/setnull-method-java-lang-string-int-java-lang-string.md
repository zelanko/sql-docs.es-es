---
description: Método setNull (java.lang.String, int, java.lang.String)
title: Método setNull (java.lang.String, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setNull (java.lang.String, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16ff77f9-7928-415c-abf6-97ed59e3e396
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c4d7666b4b743428ce2f81c7d84cd3b7caeca47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458627"
---
# <a name="setnull-method-javalangstring-int-javalangstring"></a>Método setNull (java.lang.String, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en un valor NULL, según el tipo y nombre del parámetro que se va a establecer.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType,  
                    java.lang.String sTypeName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Un objeto **String** que contiene el nombre de parámetro.  
  
 *nType*  
  
 Un código de tipo JDBC que es definido por java.sql.Types.  
  
 *sTypeName*  
  
 Un valor **String** que indica el nombre completo del parámetro que se establece.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setNull especifica este método setNull en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método setNull &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
