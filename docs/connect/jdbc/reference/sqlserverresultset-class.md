---
title: Clase SQLServerResultSet | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e0a2185037f54aa7ed975667c0bdd5fb921c845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970613"
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
  
## <a name="remarks"></a>Notas  
 Hay dos tipos de conjuntos de resultados: del lado cliente y del lado del servidor.  
  
 Los conjuntos de resultados del lado cliente se utilizan cuando los resultados se pueden ajustar a la memoria de procesos del cliente. Estos resultados proporcionan el rendimiento más rápido y el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] puede leerlos íntegramente desde la base de datos. Estos conjuntos de resultados no suponen una carga adicional en la base de datos al incurrir en la sobrecarga que implica la creación de cursores en el lado del servidor. Sin embargo, estos tipos de conjuntos de resultados no son actualizables.  
  
 Los resultados en el lado del servidor se pueden utilizar cuando los resultados no se ajustan en la memoria de procesos del cliente o cuando el conjunto de resultados no se puede actualizar. Con este tipo de conjunto de resultados, el controlador JDBC crea un cursor en lado del servidor y captura filas de forma trasparente en el conjunto de resultados a medida que el usuario se desplaza por este.  
  
 La clase SQLServerResultSet proporciona muchos métodos mediante los que puede actualizar el conjunto de resultados con cualquier tipo de datos nativos de Java y muchos tipos de objetos de Java.  
  
 Esta clase admite la desencapsulación en la clase SQLServerResultSet, la interfaz ISQLServerResultSet y la interfaz java. SQL. ResultSet. Para obtener más información, vea [contenedores e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
