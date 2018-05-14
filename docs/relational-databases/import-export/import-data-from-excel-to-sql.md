---
title: Importación de datos de Excel a SQL | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f65476db62b4d7eb617ca17cb0a400a8721fb75e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>Importación de datos de Excel a SQL Server o Azure SQL Database
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Hay varias formas de importar datos de archivos de Excel a SQL Server o a Azure SQL Database. En este artículo, se resume cada una de estas opciones y se proporcionan vínculos a instrucciones más detalladas.
-   Puede importar datos en un solo paso desde Excel a SQL mediante una de las siguientes herramientas:
    -   El Asistente para importación y exportación de SQL Server
    -   SQL Server Integration Services (SSIS)
    -   La función OPENROWSET
-   Puede importar datos en dos pasos si guarda los datos como texto y, después, usa una de las siguientes herramientas:
    -   La instrucción BULK INSERT
    -   BCP
    -   Azure Data Factory

La descripción completa de herramientas complejas y servicios como SSIS o Azure Data Factory queda fuera del ámbito de esta información general. Para obtener más información sobre la solución de su interés, siga los vínculos proporcionados.

> [!IMPORTANT]
> Para obtener información detallada sobre cómo conectarse a archivos de Excel y sobre las limitaciones y problemas conocidos a la hora de cargar datos de o a archivos de Excel, vea [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../../integration-services/load-data-to-from-excel-with-ssis.md).

## <a name="sql-server-import-and-export-wizard"></a>Asistente para importación y exportación de SQL Server

Importe datos directamente desde archivos de Excel siguiendo las páginas del Asistente para importación y exportación de SQL Server. Si lo desea, guarde la configuración de importación y exportación como un paquete de SQL Server Integration Services (SSIS) que puede personalizar y reutilizar.

![Conexión a un origen de datos de Excel](media/excel-connection.png)

Para obtener un ejemplo de uso del Asistente para importación de Excel a SQL Server, vea [Get started with this simple example of the Import and Export Wizard](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md) (Comenzar con este sencillo ejemplo del Asistente para importar y exportar).

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

Si está familiarizado con SSIS y no desea ejecutar el Asistente para importar y exportar de SQL Server, cree un paquete de SSIS que usa el origen de Excel y el destino de SQL Server en el flujo de datos.

![Componentes del flujo de datos](media/excel-to-sql-data-flow.png)

Para obtener más información sobre estos componentes de SSIS, vea los siguientes temas:
-   [Origen de Excel](../../integration-services/data-flow/excel-source.md)
-   [Destino de SQL Server](../../integration-services/data-flow/sql-server-destination.md)

Para empezar a obtener información sobre cómo compilar paquetes de SSIS, vea el tutorial [How to Create an ETL Package](../../integration-services/ssis-how-to-create-an-etl-package.md) (Creación de un paquete de ETL).

## <a name="openrowset-and-linked-servers"></a>OPENROWSET y servidores vinculados
> [!NOTE]
> El proveedor de ACE (anteriormente, el proveedor de Jet) que se conecta a los orígenes de datos de Excel está diseñado para un uso interactivo del lado cliente. Si utiliza el proveedor de ACE en el servidor, especialmente en procesos automatizados o en procesos que se ejecutan en paralelo, puede obtener resultados inesperados.

### <a name="distributed-queries"></a>Consultas distribuidas

Importe datos directamente desde archivos de Excel con la función `OPENROWSET` u `OPENDATASOURCE` de Transact-SQL. A este uso se le denomina *consulta distribuida*.

Para poder ejecutar una consulta distribuida, primero debe habilitar la opción de configuración del servidor `ad hoc distributed queries`, como se muestra en el ejemplo siguiente. Para más información, vea [ad hoc distributed queries Server Configuration Option](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md) (Opción de configuración del servidor Consultas distribuidas ad hoc).

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

En el ejemplo de código siguiente se usa `OPENROWSET` para importar los datos de la hoja de cálculo `Data` de Excel a una nueva tabla de base de datos.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=D:\Desktop\Data.xlsx', [Data$]);
GO
```

Este es el mismo ejemplo con `OPENDATASOURCE`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=D:\Desktop\Data.xlsx;Extended Properties=Excel 12.0')...[Data$];
GO
```

Para *anexar* los datos importados a una tabla *existente* en lugar de crear una tabla nueva, use la sintaxis `INSERT INTO ... SELECT ... FROM ...` en lugar de la sintaxis `SELECT ... INTO ... FROM ...` utilizada en los ejemplos anteriores.

Para consultar los datos de Excel sin importarlos, solo tiene que usar la sintaxis `SELECT ... FROM ...` estándar.

Para obtener más información sobre las consultas distribuidas, vea los temas siguientes:
-   [Consultas distribuidas](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx). (Las consultas distribuidas todavía se admiten en SQL Server 2016, pero no se ha actualizado la documentación para esta característica).
-   [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
-   [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>Servidores vinculados

También puede configurar una conexión persistente al archivo de Excel como un *servidor vinculado*. En el ejemplo siguiente se importan los datos de la hoja de cálculo `Data` del servidor vinculado a Excel existente `EXCELLINK` en una nueva tabla de base de datos denominada `Data_ls`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_ls FROM EXCELLINK...[Data$];
GO
```

Puede crear un servidor vinculado desde SQL Server Management Studio o mediante la ejecución del procedimiento almacenado del sistema `sp_addlinkedserver`, como se muestra en el ejemplo siguiente.

```sql
DECLARE @RC int

DECLARE @server     nvarchar(128)
DECLARE @srvproduct nvarchar(128)
DECLARE @provider   nvarchar(128)
DECLARE @datasrc    nvarchar(4000)
DECLARE @location   nvarchar(4000)
DECLARE @provstr    nvarchar(4000)
DECLARE @catalog    nvarchar(128)

-- Set parameter values
SET @server =     'EXCELLINK'
SET @srvproduct = 'Excel'
SET @provider =   'Microsoft.ACE.OLEDB.12.0'
SET @datasrc =    'D:\Desktop\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

Para obtener más información sobre los servidores vinculados, vea los temas siguientes:
-   [Crear servidores vinculados](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
-   [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

Para obtener más ejemplos e información sobre los servidores vinculados y las consultas distribuidas, vea los temas siguientes:
-   [Uso de Excel con consultas distribuidas y servidores vinculados de SQL Server](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
-   [Cómo importar datos de Excel en SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prerequisite---save-excel-data-as-text"></a>Requisito previo: guardar datos de Excel como texto
Para usar el resto de los métodos descritos en esta página, es decir, la instrucción BULK INSERT, la herramienta BCP o Azure Data Factory, primero tiene que exportar los datos de Excel a un archivo de texto.

En Excel, seleccione **Archivo | Guardar como** y, después, seleccione **Texto (delimitado por tabulaciones) (\*.txt)** o **CSV (delimitado por comas) (\*.csv)** como el tipo de archivo de destino.

> [!TIP]
> Para obtener mejores resultados con las herramientas de importación de datos, guarde hojas que contienen solo los encabezados de columna y las filas de datos. Si los datos guardados contienen títulos de página, líneas en blanco, notas, etc., puede obtener resultados inesperados después al importar los datos.

## <a name="bulk-insert-command"></a>Comando BULK INSERT

`BULK INSERT` es un comando de Transact-SQL que se puede ejecutar desde SQL Server Management Studio. En el ejemplo siguiente, se cargan los datos del archivo delimitado por comas `Data.csv` en una tabla de base de datos existente.

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'D:\Desktop\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

Para obtener más información, vea los temas siguientes:
-   [Importar de forma masiva datos mediante BULK INSERT u OPENROWSET(BULK...)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
-   [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp-tool"></a>Herramienta BCP

BCP es un programa que se ejecuta desde el símbolo del sistema. En el ejemplo siguiente, se cargan los datos del archivo delimitado por comas `Data.csv` en la tabla de base de datos `Data_bcp` existente.

```sql
bcp.exe ImportFromExcel..Data_bcp in "D:\Desktop\data.csv" -T -c -t ,
```

Para obtener más información sobre BCP, vea los temas siguientes:
-   [Importar y exportar datos de forma masiva con la utilidad bcp](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
-   [bcp (utilidad)](../../tools/bcp-utility.md)
-   [Preparar los datos para exportar o importar de forma masiva](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="copy-wizard-azure-data-factory"></a>Asistente para copia (Azure Data Factory)
Importe datos guardados como archivos de texto siguiendo las páginas del Asistente para copia.

Para obtener más información sobre el Asistente para copia, vea los temas siguientes:
-   [Asistente para copia de Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
-   [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial)

## <a name="azure-data-factory"></a>Azure Data Factory
Si está familiarizado con Azure Data Factory y no quiere ejecutar al Asistente para copia, cree una canalización con una actividad de copia que copie el archivo de texto en SQL Server o en Azure SQL Database.

Para obtener más información sobre el uso de estos orígenes y receptores de Data Factory, vea los temas siguientes:
-   [Sistema de archivos](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
-   [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
-   [Azure SQL Database](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

Para empezar a obtener información sobre cómo copiar los datos con Azure Data Factory, vea los temas siguientes:
-   [Movimiento de datos con la actividad de copia](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
-   [Tutorial: Crear una canalización con la actividad de copia mediante Azure Portal](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="see-also"></a>Ver también
[Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../../integration-services/load-data-to-from-excel-with-ssis.md)
