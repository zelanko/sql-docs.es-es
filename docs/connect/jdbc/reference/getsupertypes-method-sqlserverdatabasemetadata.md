---
title: Método getSuperTypes (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSuperTypes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5b8e78e6-2bb0-4dc7-9c77-a5609654cb05
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a5893bb1585fba014a5bf652265d69953c6a11d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979294"
---
# <a name="getsupertypes-method-sqlserverdatabasemetadata"></a>Método getSuperTypes (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de las jerarquías del tipo definido por el usuario que se definen en un esquema determinado en esta base de datos.  
  
> [!NOTE]  
>  Este método no se admite actualmente con el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Cuando se utiliza este método, siempre devolverá un conjunto de resultados vacío.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getSuperTypes(java.lang.String catalog,  
                                        java.lang.String schemaPattern,  
                                        java.lang.String typeNamePattern)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 Objeto **String** que contiene el nombre del catálogo.  
  
 *schemaPattern*  
  
 Objeto **String** que contiene el modelo de nombre del esquema.  
  
 *tableNamePattern*  
  
 Objeto **String** que contiene el patrón de nombre de tabla.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getSuperTypes especifica este método getSuperTypes en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
