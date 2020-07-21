---
title: Empleo de una instrucción SQL para modificar datos | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a9de31bad8ef2980e7322b529a6a2b68a12355c2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026750"
---
# <a name="using-an-sql-statement-to-modify-data"></a>Empleo de una instrucción SQL para modificar datos

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
> Si desea que el controlador JDBC devuelva todos los recuentos de actualizaciones, incluidos los recuentos de actualizaciones devueltos por todos los desencadenadores activados, establezca la propiedad de cadena de conexión lastUpdateCount en "false". Para obtener más información sobre la propiedad lastUpdateCount, consulte [Establecimiento de las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).

## <a name="see-also"></a>Consulte también

[Empleo de instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)
