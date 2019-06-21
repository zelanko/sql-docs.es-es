---
title: Método getAttributes (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getAttributes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4dc784ed-4699-4197-9af5-6e03da80d14c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fcd33cbb39286c03b5b809b847a8d8a2b8b609f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799954"
---
# <a name="getattributes-method-sqlserverdatabasemetadata"></a>Método getAttributes (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción del atributo determinado del tipo determinado para un tipo definido por el usuario que está disponible en el esquema y catálogos determinados.  
  
> [!NOTE]  
>  El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no admite este método actualmente. Si se llama, siempre devolverá un conjunto de resultados vacío.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getAttributes(java.lang.String catalog,  
                                        java.lang.String schemaPattern,  
                                        java.lang.String typeNamePattern,  
                                        java.lang.String attributeNamePattern)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 Objeto **String** que contiene el nombre del catálogo.  
  
 *schemaPattern*  
  
 Objeto **String** que contiene el modelo de nombre del esquema.  
  
 *typeNamePattern*  
  
 Un objeto **String** que contiene el patrón de nombre de tabla.  
  
 *attributePattern*  
  
 Un objeto **String** que contiene el patrón de nombre del atributo.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getAttributes especificado por el método getAttributes en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
