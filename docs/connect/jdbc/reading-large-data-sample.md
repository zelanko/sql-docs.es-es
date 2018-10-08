---
title: Ejemplo de datos grandes de lectura | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75e2117f67969585ef8bab38b845c4ee55d9b79f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621633"
---
# <a name="reading-large-data-sample"></a>Leer un ejemplo de datos grandes

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se muestra cómo recuperar un valor grande de una sola columna desde una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el método [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md).

El archivo de código para este ejemplo se denomina ReadLargeData.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, deberá tener acceso a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. También deberá establecer la ruta de clase para incluir el archivo jar mssql-jdbc. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código realiza una conexión a la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Luego, el código muestra crea los datos del ejemplo y actualiza la tabla Production.Document con una consulta con parámetros.

Además, en el código se indica cómo establecer el modo de almacenamiento en búfer adaptable con el método [getResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Tenga en cuenta que desde la publicación de la versión 2.0 del controlador JDBC, la propiedad de conexión responseBuffering se establece en "adaptive" de manera predeterminada.

Después, con una instrucción SQL con el objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), el código ejecuta la instrucción SQL y coloca los datos que devuelve en un objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).

Por último, el código itera por las filas de datos que se encuentran en el conjunto de resultados y usa el método [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) para tener acceso a algunos de los datos.

[!code[JDBC#UsingAdaptiveBuffering1](../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]

## <a name="see-also"></a>Ver también

[Trabajo con datos grandes](../../connect/jdbc/working-with-large-data.md)
