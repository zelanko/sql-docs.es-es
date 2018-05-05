---
title: Usar instrucciones con el controlador JDBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7da2ce5f69df8f28b281a935ea938b2648fa555
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-statements-with-the-jdbc-driver"></a>Usar instrucciones con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] puede utilizarse para trabajar con datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos en una variedad de formas. El controlador JDBC se puede usar para ejecutar instrucciones de SQL contra la base de datos o para llamar a procedimientos almacenados en la base de datos, empleando parámetros de entrada y de salida. El controlador JDBC también admite el uso de secuencias de escape de SQL, claves generadas automáticamente y actualizaciones realizadas dentro de una operación por lotes.  
  
 El controlador JDBC proporciona tres clases para recuperar datos de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos:  
  
1.  [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) : se usan para ejecutar instrucciones SQL sin parámetros.  
  
2.  [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) - (heredada de SQLServerStatement), utilizado para la ejecución de instrucciones SQL compiladas que puede contener parámetros IN.  
  
3.  [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) - (heredada de SQLServerPreparedStatement), usadas para ejecutar procedimientos almacenados que pueden contener parámetros IN, OUT parámetros, o ambos.  
  
 Los temas de esta sección tratan cómo usar cada una de las tres clases de instrucciones para trabajar con datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Usar instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)|Describe cómo usar instrucciones SQL con el controlador JDBC para trabajar con datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.|  
|[Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)|Describe cómo utilizar procedimientos almacenados con el controlador JDBC para trabajar con datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.|  
|[Usar varios conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md)|Describe cómo usar el controlador JDBC para recuperar datos de varios conjuntos de resultados.|  
|[Usar secuencias de escape SQL](../../connect/jdbc/using-sql-escape-sequences.md)|Describe cómo usar secuencias de escape de SQL, como literales y funciones de fecha y hora.|  
|[Usar claves generadas automáticamente](../../connect/jdbc/using-auto-generated-keys.md)|Describe cómo usar claves generadas automáticamente.|  
|[Realizar operaciones por lotes](../../connect/jdbc/performing-batch-operations.md)|Describe cómo usar el controlador JDBC para llevar a cabo operaciones en lote.|  
|[Controlar instrucciones complejas](../../connect/jdbc/handling-complex-statements.md)|Describe cómo usar el controlador JDBC para ejecutar instrucciones complejas que realizan diversas tareas y pueden devolver tipos diferentes de datos.|  
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
