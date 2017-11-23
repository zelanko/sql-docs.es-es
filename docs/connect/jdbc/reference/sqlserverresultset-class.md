---
title: Clase SQLServerResultSet | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 254aa0bfb009eb852656ca62c4cba19fc8a03e39
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverresultset-class"></a>Clase SQLServerResultSet
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa un conjunto de resultados JDBC.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final class SQLServerResultSet  
```  
  
## <a name="remarks"></a>Comentarios  
 Hay dos tipos de conjuntos de resultados: del lado cliente y del lado del servidor.  
  
 Los conjuntos de resultados del lado cliente se utilizan cuando los resultados se pueden ajustar a la memoria de procesos del cliente. Estos resultados proporcionan el rendimiento más rápido y son leídos por la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] en su totalidad de la base de datos. Estos conjuntos de resultados no suponen una carga adicional en la base de datos al incurrir en la sobrecarga que implica la creación de cursores en el lado del servidor. Sin embargo, estos tipos de conjuntos de resultados no son actualizables.  
  
 Los resultados en el lado del servidor se pueden utilizar cuando los resultados no se ajustan en la memoria de procesos del cliente o cuando el conjunto de resultados no se puede actualizar. Con este tipo de conjunto de resultados, el controlador JDBC crea un cursor en lado del servidor y captura filas de forma trasparente en el conjunto de resultados a medida que el usuario se desplaza por este.  
  
 La clase SQLServerResultSet proporciona muchos métodos que puede actualizar el conjunto de resultados con cualquier tipo de datos de Java nativo y muchos tipos de objetos de Java.  
  
 Esta clase admite la acción de desencapsular para la clase SQLServerResultSet, la interfaz de ISQLServerResultSet y la interfaz java.sql.ResultSet. Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
