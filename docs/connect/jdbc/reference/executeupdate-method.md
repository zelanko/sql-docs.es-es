---
title: Método executeUpdate () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2d949416f96c704cc721e8037bc022bdceac4291
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799015"
---
# <a name="executeupdate-method-"></a>Método executeUpdate ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL en este objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), que debe ser una instrucción INSERT, UPDATE, MERGE o DELETE de SQL; o una instrucción SQL que no devuelva nada, como una instrucción DDL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el número de filas afectadas o 0 si se usa una instrucción DDL.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método executeUpdate especifica este método executeUpdate en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método executeUpdate &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
