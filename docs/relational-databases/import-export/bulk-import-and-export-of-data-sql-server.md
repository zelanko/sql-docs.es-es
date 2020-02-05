---
title: Importar y exportar datos de forma masiva (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 462df4c5acf09d5de57a237c8fd68e5a394fb0dc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71680811"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>Importar y exportar datos de forma masiva (SQL Server)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la exportación masiva de datos (*conjuntos masivos de datos*) desde una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la importación en bloque de datos en una tabla o vista sin particiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

- La*exportación masiva* se refiere a la copia de datos de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un archivo de datos.
- *Importación masiva* significa cargar datos de un archivo de datos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por ejemplo, puede exportar datos de una aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel a un archivo de datos y, después, importarlos masivamente en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

## <a name="MethodsForBuliIE"></a> Métodos para la importación y exportación masivas de datos

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la exportación masiva de datos desde una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la importación masiva de datos en una tabla o vista sin particiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Están disponibles los métodos básicos siguientes.

|Método|Descripción|Importa datos|Exporta datos|
|------------|-----------------|------------------|------------------|
|[Utilidad bcp](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|Utilidad de línea de comandos (Bcp.exe) que importa y exporta datos masivamente y genera archivos de formato.|Sí|Sí|
|[Instrucción BULK INSERT](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que importa datos directamente de un archivo de datos en una tabla o vista sin particionar de una base de datos.|Sí|No|
|[INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que usa el proveedor de conjuntos de filas BULK OPENROWSET para importar masivamente datos en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificando la función OPENROWSET(BULK...) para seleccionar datos en una instrucción INSERT.|Sí|No|
|[Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)|El asistente crea paquetes simples que importan y exportan datos entre muchos formatos de datos conocidos, incluidas bases de datos, hojas de cálculo y archivos de texto.|Sí|Sí|

> [!IMPORTANT]
> Para obtener las reglas sobre el uso de un archivo de valores separados por comas (CSV) como archivo de datos para una importación en bloque de datos a SQL Server, vea [Preparación de los datos para exportar o importar en bloque (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).

> [!NOTE]
> Azure SQL DW solo admite la utilidad bcp para importar y exportar archivos delimitados.

## <a name="FFs"></a> Archivos de formato

La [utilidad bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)e [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) admiten el uso de un *archivo de formato* especializado que almacena información de formato para cada campo de un archivo de datos. El archivo de formato puede contener también información acerca de la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente. El archivo de formato se puede utilizar para proporcionar toda la información de formato necesaria para la exportación e importación masivas de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

> [!IMPORTANT]
> No se puede usar BCP para importar o exportar datos a Azure Blob Storage en Azure SQL Database. Use [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) para importar desde o exportar a Azure Blob Storage.

Los archivos de formato proporcionan una forma flexible de interpretar los datos con el formato que tienen en el archivo de datos durante la importación, así como para dar formato a los datos del archivo de datos durante la exportación. Esta flexibilidad elimina la necesidad de escribir código para propósitos especiales con el fin de interpretar los datos o volver a darles formato según los requisitos específicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la aplicación externa. Por ejemplo, si va a exportar masivamente datos que se van a cargar en una aplicación que requiere valores separados por comas, puede usar un archivo de formato para insertar comas como terminadores de campo en los datos exportados.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite dos tipos de archivos de formato: archivos de formato XML y no XML.

La [utilidad bcp](../../tools/bcp-utility.md) es la única herramienta que puede generar un archivo de formato. Para obtener más información, vea [Crear un archivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md). Para obtener más información sobre archivos de formato, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).

> [!NOTE]
> En aquellos casos en que no se suministra un archivo de formato durante una operación de exportación o importación masiva, puede invalidar el formato predeterminado en la línea de comandos.

|Temas relacionados|
|---|
|[Preparar los datos para exportar o importar de forma masiva (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)|
|[Formatos de datos para importación o exportación masivas (SQL Server)](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar el formato nativo para importar o exportar datos (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar el formato de caracteres para importar o exportar datos (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar el formato nativo Unicode para importar o exportar datos (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar el formato de caracteres Unicode para importar o exportar datos (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)|
|[Especificar formatos de datos por razones de compatibilidad mediante bcp (SQL Server)](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Especificar el tipo de almacenamiento en archivo mediante bcp (SQL Server)](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Especificar la longitud de prefijo en los archivos de datos mediante bcp (SQL Server)](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Especificar la longitud de campo mediante bcp (SQL Server)](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Especificar terminadores de campo y de fila (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)|
|[Mantener valores NULL o usar valores predeterminados durante la importación masiva (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)|
|[Mantener valores de identidad al importar datos de forma masiva (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)|
|[Archivos de formato para importar o exportar datos (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Crear un archivo de formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar un archivo de formato para importar datos de forma masiva (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar un archivo de formato para omitir una columna de tabla (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar un archivo de formato para omitir un campo de datos (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)|

## <a name="more-information"></a>Más información

- [Requisitos previos para el registro mínimo durante la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)
- [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
- [Copiar bases de datos en otros servidores](../../relational-databases/databases/copy-databases-to-other-servers.md)
- [Carga masiva de datos XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)
- [Realizar operaciones de copia masiva](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)
