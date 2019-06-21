---
title: Método getCatalogSeparator (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogSeparator
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0bbd6842-7210-432a-bef4-e15a63f5cc96
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d3e836a031f319c3e92227f1d51fcd436c9d3ed7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803940"
---
# <a name="getcatalogseparator-method-sqlserverdatabasemetadata"></a>Método getCatalogSeparator (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el objeto **String** que esta base de datos emplea como separador entre un nombre de catálogo y de tabla.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getCatalogSeparator()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto **String** que contiene el separador del catálogo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getCatalogSeparator especifica este método getCatalogSeparator en la interfaz java.sql.DatabaseMetaData.  
  
 Cuando el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se usa con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método devuelve un punto (".") como separador del catálogo.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
