---
title: Importar y exportar datos de SQL Server y de Azure SQL Database | Microsoft Docs
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 1d37d86ab2e2bac04ceb8ce36fad63ae25f0f92b
ms.contentlocale: es-es
ms.lasthandoff: 10/18/2017

---
# <a name="import-and-export-data-from-sql-server-and-azure-sql-database"></a>Importar y exportar datos de SQL Server y de Azure SQL Database
Puede usar diversos métodos para importar y exportar datos de SQL Server y Azure SQL Database. Estos métodos incluyen instrucciones Transact-SQL, herramientas de línea de comandos y asistentes.

También puede importar y exportar datos en distintos formatos de datos. Estos formatos incluyen archivos planos, Excel, las principales bases de datos relacionales y distintos servicios en la nube.

## <a name="methods-for-importing-and-exporting-data"></a>Métodos para la importación y exportación de datos

### <a name="use-transact-sql-statements"></a>Uso de instrucciones Transact-SQL
Puede importar datos con los comandos `BULK INSERT` u `OPENROWSET(BULK...)`. Normalmente, estos comandos se ejecutan en SQL Server Management Studio (SSMS). Para más información, vea [Importar de forma masiva datos mediante BULK INSERT u OPENROWSET(BULK...)](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

### <a name="use-bcp-from-the-command-prompt"></a>Usar BCP desde el símbolo del sistema
Puede importar y exportar datos con la utilidad de línea de comandos BCP. Para más información, vea [Importar y exportar datos de forma masiva con la utilidad bcp](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

### <a name="use-the-import-flat-file-wizard"></a>Uso del Asistente para la importación de archivos planos
Si no necesita todas las opciones de configuración disponibles en el Asistente para importación y exportación y otras herramientas, puede importar un archivo de texto en SQL Server con el **Asistente para importación de archivos planos** en SQL Server Management Studio (SSMS). Para obtener más información, vea los artículos siguientes:
- [What’s new in SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/) (Novedades en SQL Server Management Studio 17.3)
- [Introducing the new Import Flat File Wizard in SSMS 17.3](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173) (Introducción al nuevo Asistente para importación de archivos planos en SSMS 17.3)

### <a name="use-the-sql-server-import-and-export-wizard"></a>Usar el Asistente para importación y exportación de SQL Server
Puede importar o exportar datos desde una variedad de orígenes y destinos con el Asistente para importación y exportación de SQL Server. Para usar el asistente debe tener instalado SQL Server Integration Services (SSIS) o SQL Server Data Tools (SSDT). Para más información, vea [Importar y exportar datos con el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

### <a name="design-your-own-import-or-export"></a>Diseñar su propia importación o exportación
Si quiere diseñar una importación de datos personalizada, puede usar una de las siguientes características o servicios:
-   SQL Server Integration Services. Para más información, vea [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).
-   Azure Data Factory. Para más información, vea [Introducción a Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-introduction).

## <a name="data-formats-for-import-and-export"></a>Formatos de datos para la importación y la exportación

### <a name="supported-formats"></a>Formatos admitidos

Puede importar y exportar datos a archivos planos o a muchos otros formatos de archivos, bases de datos relacionales y servicios en la nube. Para obtener más información sobre estas opciones para herramientas específicas, vea los temas siguientes.
-   Para el Asistente para importación y exportación de SQL Server, vea [Conectarse a orígenes de datos con el Asistente para importar y exportar de SQL Server](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md).
-   Para SQL Server Integration Services, vea [Conexiones de Integration Services (SSIS)](../../integration-services/connection-manager/integration-services-ssis-connections.md).
-   Para Azure Data Factory, vea [Conectores de Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-amazon-redshift-connector).

### <a name="commonly-used-data-formats"></a>Formatos de datos de uso frecuente

Hay ejemplos y consideraciones especiales para algunos formatos de datos de uso común. Para obtener más información sobre estos formatos de datos, vea los temas siguientes:
-   Para Excel, vea [Importar desde Excel](import-data-from-excel-to-sql.md).
-   Para JSON, vea [Importar documentos JSON](../json/import-json-documents-into-sql-server.md).
-   Para XML, vea [Importar y exportar documentos XML](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md).
-   Para Azure Blob Storage, vea [Importar y exportar desde Azure Blob Storage](examples-of-bulk-access-to-data-in-azure-blob-storage.md).

## <a name="next-steps"></a>Pasos siguientes
Si no está seguro de por dónde debe comenzar con la tarea de importación o exportación, plantéese usar el Asistente para importación y exportación de SQL Server. Para obtener una introducción rápida, vea [Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

