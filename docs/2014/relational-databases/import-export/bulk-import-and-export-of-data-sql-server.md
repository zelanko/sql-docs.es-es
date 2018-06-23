---
title: Importar y exportar datos de forma masiva (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 56
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 615da1ce995a23b9518997570a9e34df71b4efb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36102868"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>Importar y exportar datos de forma masiva (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la exportación masiva de datos (*conjuntos masivos de datos*) desde una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la importación en bloque de datos en una tabla o vista sin particiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La importación y la exportación masivas son esenciales para transferir datos de forma eficaz entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y orígenes de datos heterogéneos. La*exportación masiva* se refiere a la copia de datos de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un archivo de datos. *Importación masiva* significa cargar datos de un archivo de datos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por ejemplo, puede exportar datos de una aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel a un archivo de datos y, después, importarlos masivamente en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **En este tema:**  
  
-   [Introducción a la importación en bloque y las operaciones de exportación masiva](#Intro)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="Intro"></a> Información general de exportación masiva e importación  
 En esta sección se enumeran y comparan brevemente los diferentes métodos disponibles para la importación y exportación masiva de datos. En la sección también se presentan los archivos de formato.  
  
 **En este tema:**  
  
-   [Métodos de importación y exportación de datos masiva](#MethodsForBuliIE)  
  
-   [Archivos de formato](#FFs)  
  
###  <a name="MethodsForBuliIE"></a> Métodos de importación y exportación de datos masiva  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la exportación masiva de datos desde una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la importación masiva de datos en una tabla o vista sin particiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Están disponibles los métodos básicos siguientes.  
  
|Método|Descripción|Importa datos|Exporta datos|  
|------------|-----------------|------------------|------------------|  
|[bcp, utilidad](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|Utilidad de línea de comandos (Bcp.exe) que importa y exporta datos masivamente y genera archivos de formato.|Sí|Sí|  
|[BULK INSERT, instrucción](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que importa datos directamente de un archivo de datos en una tabla o vista sin particionar de una base de datos.|Sí|no|  
|[Instrucción INSERT ... Instrucción SELECT * FROM OPENROWSET(BULK...)](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que usa el proveedor de conjuntos de filas BULK OPENROWSET para importar masivamente datos en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificando la función OPENROWSET(BULK…) para seleccionar datos en una instrucción INSERT.|Sí|no|  
  
> [!IMPORTANT]  
>  Las operaciones de importación masiva de SQL Server no admiten los archivos de valores separados por comas (CSV). Sin embargo, en algunos casos se puede usar un archivo de valores separados por comas (CSV) como archivo de datos para una importación masiva de datos en SQL Server. Tenga en cuenta que el terminador de campo de un archivo CSV no tiene que ser una coma. Para obtener más información, vea [Preparar los datos para exportar o importar en bloque &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md).  
  
###  <a name="FFs"></a> Archivos de formato  
 La utilidad **bcp**, BULK INSERT e INSERT ... SELECT \* FROM OPENROWSET(BULK...) admiten el uso de un *archivo de formato* especializado que almacena información de formato para cada campo de un archivo de datos. El archivo de formato puede contener también información acerca de la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente. El archivo de formato se puede utilizar para proporcionar toda la información de formato necesaria para la exportación e importación masivas de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los archivos de formato proporcionan una forma flexible de interpretar los datos con el formato que tienen en el archivo de datos durante la importación, así como para dar formato a los datos del archivo de datos durante la exportación. Esta flexibilidad elimina la necesidad de escribir código para propósitos especiales con el fin de interpretar los datos o volver a darles formato según los requisitos específicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la aplicación externa. Por ejemplo, si va a exportar masivamente datos que se van a cargar en una aplicación que requiere valores separados por comas, puede usar un archivo de formato para insertar comas como terminadores de campo en los datos exportados.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite dos tipos de archivos de formato: archivos de formato XML y no XML.  
  
 La utilidad **bcp** es la única herramienta que puede generar un archivo de formato. Para obtener más información, vea [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md). Para obtener más información sobre archivos de formato, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
> [!NOTE]  
>  En aquellos casos en que no se suministra un archivo de formato durante una operación de exportación o importación masiva, puede invalidar el formato predeterminado en la línea de comandos.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Importar y exportar datos de forma masiva con la utilidad bcp &#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)  
  
-   [Importar datos de forma masiva mediante BULK INSERT u OPENROWSET&#40;masiva... &#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Preparar los datos para exportar o importar en bloque &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Para usar un archivo de formato**  
  
-   [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Para usar formatos de datos para la importación o exportación masivas**  
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Para especificar formatos de datos por razones de compatibilidad cuando se usa bcp**  
  
1.  [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Requisitos previos para el registro mínimo durante la importación masiva](prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [Copiar bases de datos en otros servidores](../databases/copy-databases-to-other-servers.md)   
 [Realizar la carga masiva de datos XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [Realizar operaciones de copia masiva](../native-client/features/performing-bulk-copy-operations.md)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
