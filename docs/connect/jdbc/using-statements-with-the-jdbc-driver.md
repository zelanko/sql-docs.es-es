---
title: Usar instrucciones con el controlador JDBC | Microsoft Docs
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
ms.openlocfilehash: 7320c90f1ec0517ccc7d22a30b0678074a24e7e6
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/08/2018
ms.locfileid: "39661727"
---
# <a name="using-statements-with-the-jdbc-driver"></a>Usar instrucciones con el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se puede usar para trabajar con datos en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de distintos modos. El controlador JDBC se puede usar para ejecutar instrucciones de SQL contra la base de datos o para llamar a procedimientos almacenados en la base de datos, empleando parámetros de entrada y de salida. El controlador JDBC también admite el uso de secuencias de escape de SQL, claves generadas automáticamente y actualizaciones realizadas dentro de una operación por lotes.  
  
El controlador JDBC proporciona tres clases para la recuperación de datos desde una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
1. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), para ejecutar instrucciones de SQL sin parámetros.  
  
2. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) (heredada de SQLServerStatement), para ejecutar instrucciones de SQL compiladas que pueden contener parámetros IN.  
  
3. [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), (heredada de SQLServerPreparedStatement), para ejecutar procedimientos almacenados que pueden contener parámetros IN, OUT o de ambos tipos.  
  
 En los temas de esta sección se trata cómo usar cada una de estas tres clases de instrucciones para trabajar con datos de una base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="in-this-section"></a>En esta sección  

| Tema                                                                                                    | Descripción                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Usar instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)                             | Describe cómo usar instrucciones SQL con el controlador JDBC para trabajar con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].    |
| [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md) | Describe cómo usar procedimientos almacenados con el controlador JDBC para trabajar con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. |
| [Usar varios conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md)                           | Describe cómo usar el controlador JDBC para recuperar datos de varios conjuntos de resultados.                                                                       |
| [Usar secuencias de escape SQL](../../connect/jdbc/using-sql-escape-sequences.md)                           | Describe cómo usar secuencias de escape de SQL, como literales y funciones de fecha y hora.                                                               |
| [Usar claves generadas automáticamente](../../connect/jdbc/using-auto-generated-keys.md)                             | Describe cómo usar claves generadas automáticamente.                                                                                                     |
| [Realizar operaciones por lotes](../../connect/jdbc/performing-batch-operations.md)                         | Describe cómo usar el controlador JDBC para llevar a cabo operaciones en lote.                                                                                      |
| [Controlar instrucciones complejas](../../connect/jdbc/handling-complex-statements.md)                         | Describe cómo usar el controlador JDBC para ejecutar instrucciones complejas que realizan diversas tareas y pueden devolver tipos diferentes de datos.               |
  
## <a name="see-also"></a>Ver también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
