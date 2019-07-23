---
title: Método setTimestamp (int, java.sql.Timestamp) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTimestamp (int, java.sql.Timestamp)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2f7bb89f-ace7-41cb-b596-5aa8d0dd9e3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8b9d568f5e79ee548c92305378cc7e285c2bb3a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972430"
---
# <a name="settimestamp-method-int-javasqltimestamp"></a>Método setTimestamp (int, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado para el valor de marca de tiempo determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setTimestamp(int n,  
                               java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *n*  
  
 Valor **int** que indica el número de parámetro.  
  
 *x*  
  
 Objeto timestamp.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método setTimestamp especifica este método setTimestamp en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte también  
 [setTimestamp (método) &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
