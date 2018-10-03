---
title: Trabajar con tipos de datos (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a160da53ddc8a634953fc7f7b75028075ce3d691
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696714"
---
# <a name="working-with-data-types-jdbc"></a>Trabajar con tipos de datos (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La función principal del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] es permitir a los desarrolladores de Java el acceso a datos contenidos en bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para ello, el controlador JDBC realiza la conversión entre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los tipos y objetos en lenguaje Java.  
  
> [!NOTE]  
> Para obtener una descripción detallada de los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el controlador JDBC, incluidas sus diferencias y el modo de conversión a los tipos de datos en lenguaje Java, vea [Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
Para trabajar con los tipos de datos de SQL Server, el controlador JDBC proporciona los métodos get\<Type> y set\<Type> para las clases [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), y proporciona los métodos get\<Type> y update\<Type> para la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md). El método usado depende del tipo de datos con que se trabaja y del uso de conjuntos de resultados o consultas.  
  
En los temas de esta sección se describe cómo usar los tipos de datos del controlador JDBC para obtener acceso a los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las aplicaciones de Java.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Ejemplo de tipos de datos básicos](../../connect/jdbc/basic-data-types-sample.md)|Describe cómo usar los métodos captadores del conjunto de resultados para recuperar valores de tipos de datos básicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo usar los métodos de actualización del conjunto de resultados para actualizar dichos valores.|  
|[Ejemplos de tipos de datos SQLXML](../../connect/jdbc/sqlxml-data-type-sample.md)|Describe cómo almacenar datos XML en una base de datos relacional, cómo recuperar datos XML desde una base de datos y cómo analizar datos XML con el tipo de datos Java de **SQLXML**.|  
|[Ejemplo de tipos de datos espaciales](../../connect/jdbc/spatial-data-types-sample.md)|Describe cómo almacenar y recuperar los datos con los tipos de datos espaciales 'Geometría' y 'Geography' de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la base de datos **geometría** y **Geography** tipos de Java definidos por el controlador JDBC de Microsoft.|

## <a name="see-also"></a>Ver también

[Aplicaciones del controlador JDBC de ejemplo](../../connect/jdbc/sample-jdbc-driver-applications.md)  
