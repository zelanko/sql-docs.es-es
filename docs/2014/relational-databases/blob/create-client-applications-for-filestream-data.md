---
title: Creación de aplicaciones cliente para datos FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32
ms.assetid: 8a02aff6-e54c-40c6-a066-2083e9b090aa
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a9b4b5b41908c726f8baca6acb38a8bcacdf93a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151055"
---
# <a name="create-client-applications-for-filestream-data"></a>Crear aplicaciones cliente para datos FILESTREAM
  Puede utilizar Win32 para leer y escribir datos en un FILESTREAM BLOB. Se requieren los pasos siguientes:  
  
-   Lea la ruta de acceso al archivo FILESTREAM.  
  
-   Lea el contexto de transacción actual.  
  
-   Obtenga un identificador de Win32 y úselo para leer y escribir los datos en el FILESTREAM BLOB.  
  
> [!NOTE]  
>  Los ejemplos de este tema requieren la tabla y la base de datos habilitada para FILESTREAM que se crean en [Crear una base de datos habilitada para FILESTREAM](create-a-filestream-enabled-database.md) y [Crear una tabla para almacenar datos FILESTREAM](create-a-table-for-storing-filestream-data.md).  
  
##  <a name="func"></a> Funciones para trabajar con datos FILESTREAM  
 Al usar FILESTREAM para almacenar datos de objeto binario (BLOB), puede usar las API de Win32 para trabajar con los archivos. Para permitir trabajar con datos de FILESTREAM BLOB en aplicaciones de Win32, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona la API y las funciones siguientes:  
  
-   [PathName](/sql/relational-databases/system-functions/pathname-transact-sql) devuelve una ruta de acceso como token a un BLOB. Una aplicación usa este token para obtener un identificador de Win32 y operar en los datos BLOB.  
  
     Cuando la base de datos que contiene datos de FILESTREAM pertenece a un grupo de disponibilidad AlwaysOn, la función PathName devuelve un nombre de red virtual (VNN) en lugar de un nombre de equipo.  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) devuelve un token que representa la transacción actual de una sesión. Una aplicación usa este token para enlazar las operaciones de transmisión por secuencias del sistema de archivos FILESTREAM a la transacción.  
  
-   La [API OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md) obtiene un identificador de archivos de Win32. La aplicación usa el identificador para transmitir en secuencia los datos de FILESTREAM y, a continuación, puede pasar el identificador a las API de Win32 siguientes: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426)o [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Si la aplicación llama a cualquier otra API usando el identificador, se devuelve un error de ERROR_ACCESS_DENIED. La aplicación debería cerrar el identificador usando [CloseHandle](http://go.microsoft.com/fwlink/?LinkId=86428).  
  
 Todo el acceso al contenedor de datos FILESTREAM se realiza en una transacción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[tsql](../../includes/tsql-md.md)] se pueden ejecutar en la misma transacción para mantener la coherencia entre los datos de SQL y FILESTREAM.  
  
##  <a name="steps"></a> Pasos para tener acceso a los datos de FILESTREAM  
  
###  <a name="path"></a> Leer la ruta de acceso al archivo FILESTREAM  
 Cada celda de una tabla FILESTREAM tiene una ruta de acceso al archivo que está asociada a él. Para leer la ruta de acceso, use el `PathName` propiedad de un `varbinary(max)` columna en un [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción. El ejemplo siguiente muestra cómo leer la ruta de acceso de un `varbinary(max)` columna.  
  
 [!code-sql[FILESTREAM#FS_PathName](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_pathname)]  
  
###  <a name="trx"></a> Leer el contexto de transacción  
 Para obtener el contexto de transacción actual, use la función de [!INCLUDE[tsql](../../includes/tsql-md.md)] [GET_FILESTREAM_TRANSACTION_CONTEXT()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) . En el ejemplo siguiente se muestra cómo iniciar una transacción y leer el contexto de transacción actual.  
  
 [!code-sql[FILESTREAM#FS_GET_TRANSACTION_CONTEXT](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_get_transaction_context)]  
  
###  <a name="handle"></a> Obtener un identificador de archivos de Win32  
 Para obtener un identificador de archivos de Win32, llame a la API de OpenSqlFilestream. Esta API se exporta del archivo sqlncli.dll. El identificador devuelto se puede pasar a cualquiera de las API de Win32 siguientes: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426)o [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Los ejemplos siguientes muestran cómo obtener un identificador de archivos de Win32 y cómo usarlo para leer y escribir datos en un BLOB FILESTREAM.  
  
 [!code-csharp[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cs/filestream.cs#fs_cs_readandwriteblob)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/vb/filestream.vb#fs_vb_readandwriteblob)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_writeblob)]  
  
##  <a name="best"></a> Prácticas recomendadas para el diseño y la implementación de aplicaciones  
  
-   Cuando diseñe e implemente aplicaciones que usen FILESTREAM, tenga en cuenta las directrices siguientes:  
  
-   Use NULL en lugar de 0x para representar una columna FILESTREAM no inicializada. El valor 0x hace que se cree un archivo, mientras que el valor NULL no.  
  
-   Evite operaciones de inserción y eliminación en tablas que contengan columnas FILESTREAM que no admitan valores NULL. Las operaciones de inserción y eliminación pueden modificar las tablas FILESTREAM que se usan para la recolección de elementos no utilizados. Esto puede producir el descenso del rendimiento de una aplicación a lo largo del tiempo.  
  
-   En aplicaciones que usan la replicación, use NEWSEQUENTIALID() en lugar de NEWID(). NEWSEQUENTIALID() se comporta mejor que NEWID() para la generación de identificadores GUID en estas aplicaciones.  
  
-   La API de FILESTREAM está diseñada para el acceso de transmisión por secuencias de Win32 a datos. Evite el uso de [!INCLUDE[tsql](../../includes/tsql-md.md)] para leer o escribir objetos binarios grandes (BLOB) de FILESTREAM superiores a 2 MB. Si debe leer o escribir datos de BLOB desde [!INCLUDE[tsql](../../includes/tsql-md.md)], asegúrese de que todos los datos de BLOB se utilicen antes de intentar abrir los BLOB de FILESTREAM desde Win32. Si no se utilizan todos los datos de [!INCLUDE[tsql](../../includes/tsql-md.md)] , puede que se produzcan errores en las operaciones sucesivas de apertura y cierre de FILESTREAM.  
  
-   Evite el uso de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que actualicen, anexen o antepongan datos al BLOB de FILESTREAM. Esto hace que los datos de BLOB se coloquen en la cola de la base de datos tempdb y luego vuelvan a hacerlo en un nuevo archivo físico.  
  
-   Evite anexar actualizaciones de BLOB pequeños a un BLOB de FILESTREAM. Cada anexión hace que se copien los archivos FILESTREAM subyacentes. Si una aplicación tiene que anexar BLOBs pequeños, escríbalos en una `varbinary(max)` columna y, a continuación, realizar una sola operación de escritura en el BLOB de FILESTREAM cuando el número de BLOBs alcance el límite predeterminado.  
  
-   Evite recuperar la longitud de datos de numerosos archivos BLOB en una aplicación. Esta operación consume mucho tiempo porque el tamaño no se almacena en el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Si debe determinar la longitud de un archivo de blob, use la función DATALENGTH() de [!INCLUDE[tsql](../../includes/tsql-md.md)] para determinar el tamaño del blob si está cerrado. DATALENGTH() no abre el archivo de blob para determinar su tamaño.  
  
-   Si una aplicación usa el protocolo SMB1 (Bloque de mensajes 1), los datos de BLOB de FILESTREAM se deben leer en múltiplos de 60 KB para optimizar el rendimiento.  
  
## <a name="see-also"></a>Vea también  
 [Evitar conflictos con operaciones de base de datos en aplicaciones FILESTREAM](avoid-conflicts-with-database-operations-in-filestream-applications.md)   
 [Obtener acceso a los datos FILESTREAM con OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md)   
 [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)   
 [Realizar actualizaciones parciales de los datos FILESTREAM](make-partial-updates-to-filestream-data.md)  
  
  
