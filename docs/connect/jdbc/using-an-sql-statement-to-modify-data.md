---
title: Usar una instrucción SQL para modificar datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89fd14cf4245a3c44dad41b4af5b3b14e779e82b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838298"
---
# <a name="using-an-sql-statement-to-modify-data"></a>Usar una instrucción SQL para modificar datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para modificar los datos incluidos en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una instrucción SQL, puede usar el método [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). El método executeUpdate pasa la instrucción SQL a la base de datos para su procesamiento y luego devuelve un valor que indica el número de filas afectadas.

Para ello, primero debe crear un objeto SQLServerStatement mediante el método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

En el siguiente ejemplo, se pasa una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la función, se genera una instrucción SQL que agrega datos nuevos a la tabla y luego la instrucción se ejecuta y se muestra el valor devuelto.

[!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]

> [!NOTE]  
> Si necesita usar una instrucción SQL que contenga parámetros para modificar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe usar el método [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).
>
> Si la columna en que intenta insertar datos contiene caracteres especiales (por ejemplo, espacios), debe proporcionar los valores que se van a insertar incluso si se trata de valores predeterminados. En caso contrario, la operación de inserción no funciona.
>
> Si desea que el controlador JDBC devuelva todos los recuentos de actualizaciones, incluidos los recuentos de actualizaciones devueltos por todos los desencadenadores activados, establezca la propiedad de cadena de conexión lastUpdateCount en "false". Para obtener más información acerca de la propiedad lastUpdateCount, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).

## <a name="see-also"></a>Ver también

[Usar instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)
