---
title: Leer datos grandes con un ejemplo de procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea3143d2fd8e595d2baa7c2bad7aabeabeff8191
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39451749"
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>Leer datos grandes con un ejemplo de procedimientos almacenados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se muestra cómo recuperar un parámetro OUT grande desde un procedimiento almacenado.

El archivo de código para este ejemplo se denomina ExecuteStoredProcedure.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, deberá tener acceso a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. También deberá establecer la ruta de clase para incluir el archivo jar mssql-jdbc. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

El ejemplo crearía el procedimiento almacenado necesario en el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo:

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código realiza una conexión a la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Luego, el código muestra crea los datos del ejemplo y actualiza la tabla Production.Document con una consulta con parámetros. Después, el código establece el modo de almacenamiento en búfer adaptable con el método [getResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) y ejecuta el procedimiento almacenado GetLargeDataValue. A partir de la versión JDBC Driver 2.0, la propiedad de conexión responseBuffering se establece en "adaptive" de manera predeterminada.

Finalmente, el código muestra los datos devueltos con los parámetros OUT y cómo usar los métodos `mark` y `reset` en el flujo para volver a leer cualquier parte de los datos.

[!code[JDBC#UsingAdaptiveBuffering2](../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]

## <a name="see-also"></a>Ver también

[Trabajo con datos grandes](../../connect/jdbc/working-with-large-data.md)
