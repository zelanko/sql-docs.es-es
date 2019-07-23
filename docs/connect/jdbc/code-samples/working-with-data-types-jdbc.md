---
title: Trabajar con tipos de datos (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f49cdf12c4aaca9633670f7688783407acb05342
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957048"
---
# <a name="working-with-data-types-jdbc"></a>Trabajar con tipos de datos (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

La función principal del [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] es permitir a los desarrolladores de Java el acceso a datos contenidos en bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para ello, el controlador JDBC realiza la conversión entre los tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y los tipos y objetos en lenguaje Java.  
  
> [!NOTE]  
> Para obtener una descripción detallada de los tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el controlador JDBC, incluidas sus diferencias y el modo de conversión a los tipos de datos en lenguaje Java, vea [Describir los tipos de datos del controlador JDBC](../../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
Para trabajar con los tipos de datos de SQL Server, el controlador JDBC proporciona los métodos get\<Type> y set\<Type> para las clases [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md), y proporciona los métodos get\<Type> y update\<Type> para la clase [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md). El método usado depende del tipo de datos con que se trabaja y del uso de conjuntos de resultados o consultas.  
  
En los temas de esta sección se describe cómo usar los tipos de datos del controlador JDBC para obtener acceso a los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en las aplicaciones de Java.  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                         | Descripción                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Ejemplo de tipos de datos básicos](../../../connect/jdbc/code-samples/basic-data-types-sample.md)   | Describe cómo usar los métodos captadores del conjunto de resultados para recuperar valores de tipos de datos básicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y cómo usar los métodos de actualización del conjunto de resultados para actualizar dichos valores.                                             |
| [Ejemplos de tipos de datos SQLXML](../../../connect/jdbc/code-samples/sqlxml-data-type-sample.md)   | Describe cómo almacenar datos XML en una base de datos relacional, cómo recuperar datos XML desde una base de datos y cómo analizar datos XML con el tipo de datos Java de **SQLXML**.                                                                                   |
| [Ejemplo de tipos de datos espaciales](../../../connect/jdbc/code-samples/spatial-data-types-sample.md) | Describe cómo almacenar los tipos de datos espaciales en SQL Server y cómo recuperarlos de nuevo desde SQL Server. También describe cómo usar la **geometría** y la **geografía** de clases recién definidas del controlador para administrar la referencia de Java de estos tipos de objeto. |
  
## <a name="see-also"></a>Consulte también

[Aplicaciones del controlador JDBC de ejemplo](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
