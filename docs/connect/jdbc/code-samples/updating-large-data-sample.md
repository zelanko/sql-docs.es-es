---
title: Actualización de ejemplo de datos de gran tamaño | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c51577cb661fd085a198bacfcfa8ffdcf49e4f58
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39451891"
---
# <a name="updating-large-data-sample"></a>Actualizar un ejemplo de datos grandes

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se muestra cómo actualizar una columna grande en una base de datos.

El archivo de código para este ejemplo se denomina UpdateLargeData.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, deberá tener acceso a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. También deberá establecer la ruta de clase para incluir el archivo sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc4.jar, la aplicación de ejemplo produce la excepción común "Clase no encontrada". Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar y sqljdbc42.jar que hay que usar en función de la configuración preferida de Java Runtime Environment (JRE). En este ejemplo se usan los métodos [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) y [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md), que se incluyen en la API de JDBC 4.0, para obtener acceso a los métodos de almacenamiento en búfer de respuestas específicos del controlador. Para compilar y ejecutar este ejemplo, necesitará la biblioteca de clases sqljdbc4.jar, que proporciona compatibilidad con JDBC 4.0. Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código realiza una conexión a la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Después, el código crea un objeto Statement y usa el método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) para comprobar si el objeto es un contenedor de la clase [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) especificada. El método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) se usa para obtener acceso a los métodos de almacenamiento en búfer de respuestas específicos del controlador.

Después, el código establece el modo de almacenamiento en búfer de respuestas como "**adaptive**" mediante el uso del método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), además de mostrar cómo obtener el modo de almacenamiento en búfer adaptable.

Después, ejecuta la instrucción SQL y coloca los datos que devuelve en un objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) actualizable.

Finalmente, el código itera por las filas de datos que se encuentran en el conjunto de resultados. Si encuentra un resumen de documento vacío, usa la combinación de los métodos [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) y [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para actualizar las filas de datos y vuelve a almacenar los datos en la base de datos. Si ya hay datos, usa el método [getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) para mostrar algunos de los datos.

El comportamiento predeterminado del controlador es "**adaptive**". Aun así, para los conjuntos de resultados adaptables de solo avance y cuando los datos del conjunto de resultados son mayores que la memoria de la aplicación, la aplicación tiene que configurar explícitamente el modo de almacenamiento en búfer adaptable mediante el método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).

[!code[JDBC#UsingAdaptiveBuffering3](../../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]

## <a name="see-also"></a>Ver también

[Trabajo con datos grandes](../../../connect/jdbc/code-samples/working-with-large-data.md)
