---
description: Método updateBytes (int, byte)
title: Método updateBytes (int, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes (int, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 625f48ba-53d0-45a6-8fcb-643f1e0cbe8a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b21eb14869be6c97f07e058e8917797d61fae72e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458107"
---
# <a name="updatebytes-method-int-byte"></a>Método updateBytes (int, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con una matriz de valores **byte** según el índice de columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateBytes(int index,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Valor **int** que indica el índice de la columna.  
  
 *x*  
  
 Una matriz de valores de **byte**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método updateBytes especifica este método updateBytes en la interfaz java.sql.ResultSet.  
  
 En una versión anterior de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], se podía usar SQLServerResultSet.updateBytes para convertir valores entre matrices de bytes y tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**date**, **time**, **datetime2** o **datetimeoffset**. Ahora, al usar este método con esos tipos de datos, se producirá una excepción que indica que no se admite la conversión.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateBytes &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
