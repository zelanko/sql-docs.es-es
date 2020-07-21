---
title: Lectura de datos grandes con un ejemplo de procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 924bcf388ddf74f3be3f4bb13f83e00789fb8777
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028305"
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>Lectura de datos grandes con un ejemplo de procedimientos almacenados

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se muestra cómo recuperar un parámetro OUT grande desde un procedimiento almacenado.

El archivo de código para este ejemplo se denomina ExecuteStoredProcedure.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, deberá tener acceso a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. También establezca la ruta de clase para incluir el archivo jar mssql-jdbc. Para obtener más información sobre cómo establecer la ruta de acceso de clase, consulte [Usar el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información sobre el archivo JAR que se debe seleccionar, vea [Requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

Cree el siguiente procedimiento almacenado en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetLargeDataValue
  (@Document_ID int,
   @Document_ID_out int OUTPUT,
   @Document_Title varchar(50) OUTPUT,  
   @Document_Summary nvarchar(max) OUTPUT)  

AS
BEGIN
   SELECT @Document_ID_out = DocumentID,
          @Document_Title = Title,  
          @Document_Summary = DocumentSummary
    FROM  Production.Document  
    WHERE DocumentID = @Document_ID  
END  
```

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código realiza una conexión a la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Luego, el código muestra crea los datos del ejemplo y actualiza la tabla Production.Document con una consulta con parámetros. Después, el código establece el modo de almacenamiento en búfer adaptable con el método [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) y ejecuta el procedimiento almacenado GetLargeDataValue. Tenga en cuenta que desde la publicación de la versión 2.0 del controlador JDBC, la propiedad de conexión responseBuffering se establece en "adaptive" de manera predeterminada.

Finalmente, el código muestra los datos devueltos con los parámetros OUT y cómo usar los métodos `mark` y `reset` en el flujo para volver a leer cualquier parte de los datos.

[!code[JDBC#UsingAdaptiveBuffering2](../../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]

## <a name="see-also"></a>Consulte también

[Trabajo con datos grandes](../../../connect/jdbc/code-samples/working-with-large-data.md)
