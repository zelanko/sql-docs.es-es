---
title: Método getSchemas (String, String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76c5831547178b33854465d38cfe97dc87684d15
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684613"
---
# <a name="getschemas-method-string-string"></a>Método getSchemas (String, String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera los nombres de esquema que están disponibles en la base de datos actual a través del nombre del catálogo y de esquema especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public ResultSet getSchemas(java.lang.String catalog,  
                       java.lang.String schemaPattern)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 El nombre de un catálogo en la base de datos. Si es una cadena vacía "", el resultado incluye los esquemas sin un catálogo. Si es **null**, el nombre del catálogo no se utiliza en la búsqueda.  
  
 *schemaPattern*  
  
 El nombre de un esquema. Si es **null**, el nombre del esquema no se utiliza en la búsqueda.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getSchemas especifica este método getSchemas en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getSchemas contiene la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**String**|Nombre del esquema.|  
|TABLE_CATALOG|**String**|Nombre del catálogo para el esquema.|  
  
 Los resultados se ordenan según TABLE_CATALOG y después, según TABLE_SCHEM. En cada fila TABLE_SCHEM es la primera columna y TABLE_CATALOG la segunda.  
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
