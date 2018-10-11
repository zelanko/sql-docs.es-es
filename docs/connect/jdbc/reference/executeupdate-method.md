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
manager: craigg
ms.openlocfilehash: 0839ad771e067552b6c19d3d44c5893189a2c52d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782935"
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
 Este método executeUpdate especificado por el método executeUpdate de la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Ver también  
 [Método executeUpdate &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
