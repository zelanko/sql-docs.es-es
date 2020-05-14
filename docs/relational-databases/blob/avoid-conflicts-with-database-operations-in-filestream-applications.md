---
title: 'Evitar conflictos: operaciones de base de datos de FILESTREAM | Microsoft Docs'
description: Las aplicaciones que leen o escriben datos BLOB de FILESTREAM pueden encontrar errores de conflicto con instrucciones de Transact-SQL. Sepa cómo evitar estos tipos de conflictos.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32 and Transact-SQL Conflicts
ms.assetid: 8b1ee196-69af-4f9b-9bf5-63d8ac2bc39b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3641401fbb2314bf4712cc524777a490ced01541
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000245"
---
# <a name="avoid-conflicts-with-database-operations-in-filestream-applications"></a>Evitar conflictos con operaciones de base de datos en aplicaciones FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Las aplicaciones que usan SqlOpenFilestream() para abrir los identificadores de archivos de Win32 con el fin de leer o escribir datos BLOB de FILESTREAM pueden encontrar errores de conflictos con las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se administran en una transacción común. Esto incluye las consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] o MARS que tardan mucho en finalizar la ejecución. Las aplicaciones deben diseñarse cuidadosamente para ayudar a evitar estos tipos de conflictos.  
  
 Cuando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] o las aplicaciones intentan abrir BLOB de FILESTREAM, [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba el contexto de transacciones asociado. [!INCLUDE[ssDE](../../includes/ssde-md.md)] permite o deniega la solicitud en función de si la operación abierta opera con instrucciones DDL, instrucciones DML, la recuperación de los datos o la administración de las transacciones. La tabla siguiente muestra cómo [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina si una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] se permitirá o denegará según el tipo de archivos que se abran en la transacción.  
  
|Instrucciones Transact-SQL|Abierto para lectura|Abierto para escritura|  
|------------------------------|---------------------|----------------------|  
|Instrucciones DDL que trabajan con los metadatos de la base de datos, como CREATE TABLE, CREATE INDEX, DROP TABLE y ALTER TABLE.|Permitida|Se bloquean y agotan el tiempo de espera con un error.|  
|Instrucciones DML que trabajan con los datos que están almacenados en la base de datos, como UPDATE, DELETE e INSERT.|Permitida|Denegado|  
|SELECT|Permitida|Permitida|  
|COMMIT TRANSACTION|Denegado*|Denegado*|  
|SAVE TRANSACTION|Denegado*|Denegado*|  
|ROLLBACK|Permitido*|Permitido*|  
  
 \* La transacción se cancela y se invalidan los identificadores abiertos para el contexto de transacciones. La aplicación debe cerrar todos los identificadores abiertos.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cómo las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] y el acceso FILESTREAM de Win32 pueden producir conflictos.  
  
### <a name="a-opening-a-filestream-blob-for-write-access"></a>A. Abrir un BLOB de FILESTREAM para acceso de escritura  
 En el ejemplo siguiente se muestra el efecto de abrir únicamente un archivo para acceso de escritura.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//Write some date to the FILESTREAM BLOB.  
WriteFile(dstHandle, updateData, ...);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed. The FILESTREAM BLOB is  
//returned without the modifications that are made by  
//WriteFile(dstHandle, updateData, ...).  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed. The FILESTREAM BLOB  
//is returned with the updateData applied.  
```  
  
### <a name="b-opening-a-filestream-blob-for-read-access"></a>B. Abrir un BLOB de FILESTREAM para acceso de lectura  
 En el ejemplo siguiente se muestra el efecto de abrir únicamente un archivo para acceso de lectura.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed. Any changes that are  
//made to the FILESTREAM BLOB will not be returned until  
//the dstHandle is closed.  
//SELECT statements will be allowed.  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="c-opening-and-closing-multiple-filestream-blob-files"></a>C. Abrir y cerrar varios archivos BLOB de FILESTREAM  
 Si hay varios archivos abiertos, se usa la regla más restrictiva. En el ejemplo siguiente se abren dos archivos. El primero se abre durante la lectura y el segundo para la escritura. Se denegarán las instrucciones DML hasta que se abra el segundo archivo.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
  
dstHandle1 =  OpenSqlFilestream(dstFilePath1, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
//Close the read handle. The write handle is still open.  
CloseHandle(dstHandle);  
//DML statements are still denied because the write handle is open.  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
CloseHandle(dstHandle1);  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="d-failing-to-close-a-cursor"></a>D. No se puede cerrar un cursor  
 El ejemplo siguiente muestra cómo un cursor de instrucción que no se cierra puede evitar que `OpenSqlFilestream()` abra el BLOB para acceso de escritura.  
  
```  
TCHAR *sqlDBQuery =  
TEXT("SELECT GET_FILESTREAM_TRANSACTION_CONTEXT(),")  
TEXT("Chart.PathName() FROM Archive.dbo.Records");  
  
//Execute a long-running Transact-SQL statement. Do not allow  
//the statement to complete before trying to  
//open the file.  
  
SQLExecDirect(hstmt, sqlDBQuery, SQL_NTS);  
  
//Before you call OpenSqlFilestream() any open files  
//that the Cursor the Transact-SQL statement is using  
// must be closed. In this example,  
//SQLCloseCursor(hstmt) is not called so that  
//the transaction will indicate that there is a file  
//open for reading. This will cause the call to  
//OpenSqlFilestream() to fail because the file is  
//still open.  
  
HANDLE srcHandle =  OpenSqlFilestream(srcFilePath,  
     Write, 0,  transactionToken,  cbTransactionToken,  0);  
  
//srcHandle will == INVALID_HANDLE_VALUE because the  
//cursor is still open.  
```  
  
## <a name="see-also"></a>Consulte también  
 [Obtener acceso a los datos FILESTREAM con OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Usar conjuntos de resultados activos múltiples &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
  
  
