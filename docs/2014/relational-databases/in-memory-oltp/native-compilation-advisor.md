---
title: Asistente de compilación nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql12.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b72f500a425b7a55cab285a881c3ff915b9fb82
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358707"
---
# <a name="native-compilation-advisor"></a>Asistente de compilación nativa
  La herramienta de informes de rendimiento de transacciones (vea [Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) le informa sobre los procedimientos almacenados interpretados de la base de datos que se beneficiarían si se convierten para utilizar la compilación nativa. Después de identificar el procedimiento almacenado que desea convertir para que utilice la compilación nativa, puede utilizar el Asistente de compilación nativa para que le ayude a migrar el procedimiento almacenado interpretado a la compilación nativa. Para obtener más información acerca de los procedimientos almacenados compilados de forma nativa, vea [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md).  
  
 Para empezar, conéctese a la instancia que contiene el procedimiento almacenado interpretado. Puede conectarse a una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] . Sin embargo, si desea realizar una operación de migración con el asistente, debe conectarse a una instancia de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] que tenga habilitada la funcionalidad de OLTP en memoria. Para obtener más información acerca de los requisitos de OLTP en memoria, vea [Requirements for Using Memory-Optimized Tables](memory-optimized-tables.md).  
  
 Para obtener más información sobre las metodologías de migración, vea [OLTP en memoria: patrones de carga de trabajo comunes y consideraciones sobre la migración](https://msdn.microsoft.com/library/dn673538.aspx).  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>Tutorial del uso del Asistente de compilación nativa  
 En el **Explorador de objetos**, haga clic con el botón secundario en el procedimiento almacenado que desea convertir, y seleccione **Asistente de compilación nativa**. Se mostrará la página de bienvenida del **Asistente de compilación nativa de procedimiento almacenado**. Para continuar, haga clic en **Siguiente** .  
  
### <a name="stored-procedure-validation"></a>Validación del procedimiento almacenado  
 Esta página le indicará si el procedimiento almacenado utiliza construcciones que no son compatibles con la compilación nativa. Puede hacer clic en **Siguiente** para ver los detalles. Si hay construcciones que no son compatibles con la compilación nativa, puede hacer clic en **Siguiente** para ver los detalles.  
  
### <a name="stored-procedure-validation-result"></a>Resultado de la validación del procedimiento almacenado  
 Si hay construcciones que no son compatibles con la compilación nativa, la página **Resultado de la validación del procedimiento almacenado** mostrará los detalles. Puede generar un informe (haga clic en **Generar informe**), salir del **Asistente de compilación nativa**y actualizar el código para que sea compatible con la compilación nativa.  
  
## <a name="code-sample"></a>Ejemplo de código  
 El ejemplo siguiente muestra un procedimiento almacenado interpretado y el procedimiento almacenado equivalente para la compilación nativa. El ejemplo supone que existe un directorio denominado c:\data.  
  
```tsql  
CREATE DATABASE Demo  
ON  
PRIMARY(NAME = [Demo_data],  
FILENAME = 'C:\DATA\Demo_data.mdf', size=500MB)  
, FILEGROUP [Demo_fg] CONTAINS MEMORY_OPTIMIZED_DATA(  
NAME = [Demo_dir],  
FILENAME = 'C:\DATA\Demo_dir')  
LOG ON (name = [Demo_log], Filename='C:\DATA\Demo_log.ldf', size=500MB)  
COLLATE Latin1_General_100_BIN2;  
GO  
USE Demo;  
GO  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
  
CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
)WITH ( BUCKET_COUNT = 2097152)  
)WITH ( MEMORY_OPTIMIZED = ON )  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrderXTP] @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
(    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
     LANGUAGE = N'us_english')  
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
go  
  
select * from SalesOrders  
go  
exec dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1 ;  
exec dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2 ;  
select * from SalesOrders  
```  
  
## <a name="see-also"></a>Vea también  
 [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)  
  
  
