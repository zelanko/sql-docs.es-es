---
title: Método getUDTs (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getUDTs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4396453-dcb0-4132-8325-06b3c7896b3b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0e90f4d2ea8b98d2ecef237f04f5fe290a512c92
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765897"
---
# <a name="getudts-method-sqlserverdatabasemetadata"></a>Método getUDTs (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de los tipos definidos por el usuario que se describen en un esquema determinado.  
  
> [!NOTE]  
>  Este método no se admite actualmente con [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Cuando se utiliza este método, siempre devolverá un conjunto de resultados vacío.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getUDTs(java.lang.String catalog,  
                                  java.lang.String schemaPattern,  
                                  java.lang.String typeNamePattern,  
                                  int[] types)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 Objeto **String** que contiene el nombre del catálogo.  
  
 *schemaPattern*  
  
 Objeto **String** que contiene el modelo de nombre del esquema.  
  
 *typeNamePattern*  
  
 Un objeto **String** que contiene el patrón de nombre de tabla.  
  
 *types*  
  
 Una matriz de valores int que contiene los tipos de datos que se van a incluir. El valor NULL indica que todos los tipos deberían estar incluidos.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getUDTs especifica este método getUDTs en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
