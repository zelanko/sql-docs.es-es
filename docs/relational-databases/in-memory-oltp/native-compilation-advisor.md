---
title: Asistente de compilación nativa | Microsoft Docs
description: Aprenda a usar el Asistente de compilación nativa para migrar un procedimiento almacenado interpretado a una compilación nativa como parte de la migración a OLTP en memoria.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql13.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: efbd90e43c4f2bf7863106330b59f436c31b6238
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868538"
---
# <a name="native-compilation-advisor"></a>Asistente de compilación nativa
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Los informes de análisis de rendimiento de transacciones le informan sobre los procedimientos almacenados interpretados de la base de datos que se beneficiarían si se convierten para utilizar la compilación nativa. Para obtener más información, vea [Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md).  
  
 Después de identificar el procedimiento almacenado que desea convertir para que utilice la compilación nativa, puede utilizar el Asistente para compilación nativa (NCA) para que le ayude a migrar el procedimiento almacenado interpretado a la compilación nativa. Para obtener más información acerca de los procedimientos almacenados compilados de forma nativa, vea [Natively Compiled Stored Procedures](./a-guide-to-query-processing-for-memory-optimized-tables.md).  
  
 En un procedimiento almacenado interpretado determinado, el NCA le permite identificar todas las características que no se admiten en los módulos nativos. El NCA proporciona vínculos de documentación a soluciones alternativas o soluciones propiamente dichas.  
  
 Para obtener más información sobre las metodologías de migración, vea [OLTP en memoria: patrones de carga de trabajo comunes y consideraciones sobre la migración](/previous-versions/dn673538(v=msdn.10)).  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>Tutorial del uso del Asistente de compilación nativa  
 En el **Explorador de objetos**, haga clic con el botón secundario en el procedimiento almacenado que desea convertir, y seleccione **Asistente de compilación nativa**. Se mostrará la página de bienvenida del **Asistente de compilación nativa de procedimiento almacenado**. Haga clic en **Siguiente** para continuar.  
  
### <a name="stored-procedure-validation"></a>Validación del procedimiento almacenado  
 Esta página le indicará si el procedimiento almacenado utiliza construcciones que no son compatibles con la compilación nativa. Puede hacer clic en **Siguiente** para ver los detalles. Si hay construcciones que no son compatibles con la compilación nativa, puede hacer clic en **Siguiente** para ver los detalles.  
  
### <a name="stored-procedure-validation-result"></a>Resultado de la validación del procedimiento almacenado  
 Si hay construcciones que no son compatibles con la compilación nativa, la página **Resultado de la validación del procedimiento almacenado** mostrará los detalles. Puede generar un informe (haga clic en **Generar informe**), salir del **Asistente de compilación nativa**y actualizar el código para que sea compatible con la compilación nativa.  
  
## <a name="code-sample"></a>Ejemplo de código  
 El ejemplo siguiente muestra un procedimiento almacenado interpretado y el procedimiento almacenado *equivalente* para la compilación nativa. El ejemplo supone que existe un directorio denominado c:\data.  
  
> [!NOTE]  
>  Como de costumbre, el elemento **FILEGROUP** y la instrucción mydatabase **USE** son válidos en Microsoft SQL Server, pero no en Base de datos SQL de Azure.  
  
```sql  
CREATE DATABASE Demo  
ON  
PRIMARY(NAME = [Demo_data],  
FILENAME = 'C:\DATA\Demo_data.mdf', size=500MB)  
, FILEGROUP [Demo_fg] CONTAINS MEMORY_OPTIMIZED_DATA(  
NAME = [Demo_dir],  
FILENAME = 'C:\DATA\Demo_dir')  
LOG ON (name = [Demo_log], Filename='C:\DATA\Demo_log.ldf', size=500MB)  
COLLATE Latin1_General_100_BIN2;  
go  
  
USE Demo;  
go  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
     CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
) WITH ( BUCKET_COUNT = 2097152)  
) WITH ( MEMORY_OPTIMIZED = ON )  
go  
  
-- Interpreted.  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
-- Natively Compiled.  
CREATE PROCEDURE [dbo].[InsertOrderXTP]  
      @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
     (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
     )  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
SELECT * from SalesOrders;  
go  
  
EXECUTE dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1;  
EXECUTE dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2;  
  
SELECT * from SalesOrders;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Migrar a OLTP en memoria](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)   
 [Requisitos para usar tablas con optimización para memoria](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)  
  
