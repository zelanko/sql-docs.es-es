---
description: Método updateBytes (java.lang.String, byte)
title: Método updateBytes (java.lang.String, byte) (java.lang.String, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes (java.lang.String, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4fb9de2b-61bc-4c96-89a5-c07cd7ee201a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 566d105fd5b7fcb1dde0cb6616c02884afcc5758
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458104"
---
# <a name="updatebytes-method-javalangstring-byte"></a>Método updateBytes (java.lang.String, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con una matriz de valores **byte** según el nombre de columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateBytes(java.lang.String columnName,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 Valor **String** que contiene el nombre de columna.  
  
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
  
  
