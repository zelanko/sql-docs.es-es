---
title: Importar y exportar datos de forma masiva con la utilidad bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dd68505153eb43d826f3854bd4f525ed06ea072a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103355"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>Importar y exportar datos de forma masiva con la utilidad bcp (SQL Server)
  Este tema constituye una introducción al uso de la [utilidad bcp](../../tools/bcp-utility.md) para exportar datos desde cualquier lugar de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que funcione una instrucción SELECT, incluidas las vistas con particiones.  
  
 La utilidad bcp (Bcp.exe) es una herramienta de línea de comandos que utiliza la API de importación masiva de Bulk Copy Program o Programa de copia masiva (BCP). La utilidad bcp realiza las tareas siguientes:  
  
-   Exportaciones masivas de datos de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un archivo de datos.  
  
-   Exportaciones masivas de una consulta.  
  
-   Importaciones masivas de datos de un archivo de datos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Genera archivos de formato.  
  
 A la utilidad bcp se accede con el comando **bcp** . Para usar el comando **bcp** para realizar importaciones masivas de datos, debe conocer el esquema de la tabla y los tipos de datos de sus columnas, a menos que se use un archivo con un formato ya existente.  
  
 La utilidad bcp permite exportar datos de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un archivo de datos para usarlos en otros programas. También permite importar datos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde otro programa, normalmente otro sistema de administración de bases de datos (DBMS). Los datos se exportan primero desde el programa de origen a un archivo de datos y, después, se copian del archivo de datos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El comando **bcp** proporciona modificadores para especificar el tipo de datos del archivo de datos y otra información. Si no se especifican estos modificadores, el comando solicitará información de formato, como el tipo de campos de datos de un archivo de datos A continuación, el comando preguntará si se desea crear un archivo de formato con las respuestas interactivas. Si desea flexibilidad para operaciones futuras de importación o exportación masivas, un archivo de formato suele resultar útil. Puede especificar el archivo de formato en comandos **bcp** posteriores para archivos de datos equivalentes. Para obtener más información, vea [Especificar formatos de datos por razones de compatibilidad mediante bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
> [!NOTE]  
>  La utilidad bcp se escribe utilizando la copia masiva de ODBC  
  
 Para obtener una descripción de la sintaxis del comando **bcp** , vea [bcp Utility](../../tools/bcp-utility.md).  
  
## <a name="examples"></a>Ejemplos  
 Para consultar los ejemplos de **bcp** , vea:  
  
-   [bcp (utilidad)](../../tools/bcp-utility.md)  
  
-   [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [SELECT &#40;cláusula de Transact-SQL&#41;](/sql/t-sql/queries/select-clause-transact-sql)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [Prepararse para importar datos de forma masiva &#40;SQL Server&#41;](prepare-to-bulk-import-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Importar y exportar datos de forma masiva &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
  
