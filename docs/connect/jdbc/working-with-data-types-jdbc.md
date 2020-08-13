---
title: Trabajo con tipos de datos (JDBC)
description: Obtenga información sobre cómo trabajar con tipos de datos en el controlador JDBC para SQL Server mediante estas aplicaciones de ejemplo.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6994e7ce587cf72d7879c79604cbe3c68873ddf0
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923290"
---
# <a name="working-with-data-types-jdbc"></a>Trabajo con tipos de datos (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La función principal del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] es permitir a los desarrolladores de Java el acceso a datos contenidos en bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para ello, el controlador JDBC realiza la conversión entre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los tipos y objetos en lenguaje Java.

> [!NOTE]
> Para obtener una descripción detallada de los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el controlador JDBC, incluidas sus diferencias y cómo se convierten en tipos de datos del lenguaje Java, vea [Descripción de los tipos de datos del controlador JDBC](understanding-the-jdbc-driver-data-types.md).

Para trabajar con los tipos de datos de SQL Server, el controlador JDBC proporciona los métodos get\<Type> y set\<Type> para las clases [SQLServerPreparedStatement](reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](reference/sqlservercallablestatement-class.md), y los métodos get\<Type> y update\<Type> para la clase [SQLServerResultSet](reference/sqlserverresultset-class.md). El método usado depende del tipo de datos con que se trabaja y del uso de conjuntos de resultados o consultas.

En los temas de esta sección se describe cómo usar los tipos de datos del controlador JDBC para obtener acceso a los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las aplicaciones de Java.

## <a name="in-this-section"></a>En esta sección

|Tema|Descripción|
|-----------|-----------------|
|[Ejemplo de tipos de datos básicos](basic-data-types-sample.md)|Describe cómo usar los métodos captadores del conjunto de resultados para recuperar valores de tipos de datos básicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo usar los métodos de actualización del conjunto de resultados para actualizar dichos valores.|
|[Ejemplo de tipos de datos SQLXML](sqlxml-data-type-sample.md)|Describe cómo almacenar datos XML en una base de datos relacional, cómo recuperar datos XML desde una base de datos y cómo analizar datos XML con el tipo de datos Java de **SQLXML**.|
|[Ejemplo de tipos de datos espaciales](spatial-data-types-sample.md)|Describe cómo almacenar y recuperar datos con los tipos de datos espaciales "Geometry" y "Geography" de la base de datos con tipos de Java de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **Geometry** y **Geography** definidos por Microsoft JDBC driver.|

## <a name="see-also"></a>Consulte también

[Aplicaciones de ejemplo del controlador JDBC](sample-jdbc-driver-applications.md)
