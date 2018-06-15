---
title: Método setObject (int, java.lang.Object) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0103dfd14dd8a51263945d0048a7b6c7cb550157
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32844970"
---
# <a name="setobject-method-int-javalangobject"></a>Método setObject (int, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor del parámetro designado utilizando el objeto determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setObject(int index,  
                            java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Un **int** que indica el número de parámetro.  
  
 *obj*  
  
 Objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setObject es especificado por el método setObject en la interfaz java.sql.PreparedStatement.  
  
 Antes de llamar a este método setObject, la aplicación podría establecer el parámetro especificado mediante uno de los métodos siguientes:  
  
-   El conjunto\<tipo > métodos de la clase SQLServerPreparedStatement o de la clase SQLServerCallableStatement  
  
-   Los métodos setNull de la clase SQLServerPreparedStatement o la clase SQLServerCallableStatement  
  
-   El [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) método de la clase SQLServerCallableStatement  
  
 En tal caso, el tipo del parámetro se establece automáticamente. Si la aplicación llama a este método setObject con un valor de obj es NULL, el controlador se da por supuesto que el tipo del parámetro es uno que se establece mediante el método llamado anteriormente.  
  
 Si el valor de obj es NULL y no se puede determinar ninguna información de tipo para ese parámetro, este método setObject convierte el parámetro especificado en CHAR antes de enviarlo a la base de datos.  
  
 A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, el comportamiento de este método es modificado por la **sendTimeAsDatetime** propiedad de conexión ([estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md)) y [ SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obtener más información, consulte [java.sql.Time cómo configurar los valores se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Método setObject &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
