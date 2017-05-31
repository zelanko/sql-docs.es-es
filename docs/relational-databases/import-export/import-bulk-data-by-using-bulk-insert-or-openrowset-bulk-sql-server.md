---
title: "Importación en bloque de datos mediante las instrucciones BULK INSERT u OPENROWSET(BULK...) (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BULK INSERT statement, importing data from a remote data file
- bulk importing [SQL Server], methods
- bulk exporting [SQL Server], methods
- OPENROWSET function, BULK INSERT
- bulk importing [SQL Server], security
- bulk rowset providers [SQL Server]
- bulk exporting [SQL Server], BULK INSERT statement
- remote data access [SQL Server], bulk importing
- bulk importing [SQL Server], BULK INSERT statement
- Transact-SQL bulk export/import operations
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3abb7e7f582c7699b128d8b9d70b4aec34041424
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="import-bulk-data-by-using-bulk-insert-or-openrowsetbulk-sql-server"></a>Importación en bloque de datos mediante las instrucciones BULK INSERT o OPENROWSET(BULK...) (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  En este tema se ofrece información general acerca de cómo usar las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT e INSERT...SELECT * FROM OPENROWSET(BULK...) para realizar una importación masiva de datos desde un archivo de datos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . También se describen las consideraciones relativas a la seguridad del uso de BULK INSERT y OPENROWSET(BULK…), así como el uso de estos métodos para una importación masiva desde un origen de datos remoto.  
  
> **NOTA** Cuando use BULK INSERT o OPENROWSET(BULK…), es importante comprender el modo en que la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata la suplantación. Para obtener más información, vea la sección "Consideraciones relativas a la seguridad" más adelante en este tema.  
  
## <a name="bulk-insert-statement"></a>BULK INSERT, instrucción  
 BULK INSERT carga datos de un archivo de datos a una tabla. Esta funcionalidad es parecida a la que ofrece la opción **in** del comando **bcp** , aunque el que lee el archivo de datos es el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener una descripción de la sintaxis de BULK INSERT, vea [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## <a name="bulk-insert-examples"></a>Ejemplos de BULK INSERT  
 
  
-   [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
-   [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="openrowsetbulk-function"></a>Función OPENROWSET(BULK…)  
 Se tiene acceso al proveedor de conjuntos de filas BULK de OPENROWSET al llamar a la función OPENROWSET y especificar la opción BULK. La función OPENROWSET(BULK…) permite obtener acceso a datos remotos mediante la conexión a un origen de datos remoto como, por ejemplo, un archivo de datos, a través de un proveedor OLE DB.  

**Se aplica a:** `OPENROWSET` no está disponible en [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].
  
 Para realizar una importación masiva de datos, llame a OPENROWSET(BULK…) desde una cláusula SELECT…FROM en una instrucción INSERT. La sintaxis básica de una importación masiva de datos es:  
  
 INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
 Cuando se usa en una instrucción INSERT, OPENROWSET(BULK...) admite sugerencias de tabla. Además de las sugerencias de tabla normales, como TABLOCK, la cláusula BULK puede aceptar las sugerencias de tablas especializadas siguientes: IGNORE_CONSTRAINTS (solo pasa por alto las restricciones CHECK), IGNORE_TRIGGERS, KEEPDEFAULTS y KEEPIDENTITY. Para obtener más información, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Para obtener información sobre los usos adicionales de la opción BULK, vea [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
## <a name="insertselect--from-openrowsetbulk-statements---examples"></a>Instrucciones INSERT...SELECT * FROM OPENROWSET(BULK...), ejemplos:
  
-   [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="security-considerations"></a>Consideraciones relativas a la seguridad  
 Si un usuario utiliza un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se utilizará el perfil de seguridad de la cuenta de proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un inicio de sesión que use autenticación de SQL Server no se puede autenticar fuera del Motor de base de datos. Por tanto, cuando un inicio de sesión que usa autenticación de SQL Server inicia un comando BULK INSERT, la conexión con los datos se realiza usando el contexto de seguridad de la cuenta de proceso de SQL Server (la cuenta usada por el servicio Motor de base de datos de SQL Server). 
 
 Para leer correctamente los datos de origen, debe conceder acceso a los datos de origen a la cuenta usada por el Motor de base de datos de SQL Server. Por el contrario, si un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha iniciado sesión mediante autenticación de Windows, el usuario solo puede leer los archivos a los que la cuenta de usuario tiene acceso, independientemente del perfil de seguridad del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Por ejemplo, imagine un usuario que ha iniciado sesión en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante autenticación de Windows. Para que el usuario pueda utilizar BULK INSERT u OPENROWSET para importar datos de un archivo de datos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la cuenta de usuario necesita acceso de lectura para el archivo de datos. Como el usuario dispone de acceso al archivo de datos, podrá importar datos del archivo a la tabla, aunque el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tenga permiso de acceso al archivo. El usuario no tiene que conceder permiso de acceso a archivos al proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para permitir que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecte a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el reenvío de las credenciales de un usuario de Windows autenticado. Esto se conoce como *suplantación* o *delegación*. Es importante entender cómo la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata la seguridad en la suplantación de usuarios al utilizar BULK INSERT u OPENROWSET. La suplantación de usuarios permite que el archivo de datos resida en un equipo diferente al del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o del usuario. Por ejemplo, si un usuario del **Equipo_A** tiene acceso a un archivo de datos del **Equipo_B**y la delegación de credenciales se ha establecido correctamente, el usuario puede conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se esté ejecutando en el **Equipo_C**, tener acceso al archivo de datos del **Equipo_B**y realizar una importación en bloque de datos desde ese archivo a una tabla en el **Equipo_C**.  
  
## <a name="bulk-importing-from-a-remote-data-file"></a>Importación masiva desde un archivo de datos remoto  
 Para usar BULK INSERT o INSERT...SELECT \* FROM OPENROWSET(BULK...) para la importación en bloque de datos desde otro equipo, el archivo de datos debe estar compartido entre los dos equipos. Para especificar un archivo de datos compartido, use la convención de nomenclatura universal (UNC) para el nombre, que tiene la forma general de **\\\\***nombreDeServidor***\\***nombreDeRecursoCompartido***\\***rutaDeAcceso***\\***nombreDeArchivo*. Además, la cuenta usada para obtener acceso al archivo de datos debe tener los permisos necesarios para leer el archivo en el disco remoto.  
  
 Por ejemplo, la siguiente instrucción `BULK INSERT` realiza la importación masiva de datos en una tabla `SalesOrderDetail` de la base de datos `AdventureWorks` desde un archivo de datos denominado `newdata.txt`. Este archivo de datos reside en una carpeta compartida llamada `\dailyorders` en un directorio compartido de red llamado `salesforce` de un sistema llamado `computer2`.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';  
GO  
```  
  
> **NOTA** Esta restricción no se aplica a la utilidad **bcp** debido a que el cliente lee el archivo independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;cláusula de Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  

