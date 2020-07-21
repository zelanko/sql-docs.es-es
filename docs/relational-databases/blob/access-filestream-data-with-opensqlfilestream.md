---
title: Obtener acceso a los datos FILESTREAM con OpenSqlFilestream | Microsoft Docs
description: Descubra cómo obtener acceso a los datos FILESTREAM con OpenSqlFilestream. Vea ejemplos en los que se muestra cómo usar esta API para obtener un manipulador de Win32.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
apiname:
- OpenSqlFilestream
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0f2f87e037f16d2d0dc46d9f677403076148868b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85745178"
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>Obtener acceso a los datos FILESTREAM con OpenSqlFilestream
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La API OpenSqlFilestream obtiene un identificador de archivos de Win32 compatible para un objeto binario grande (BLOB) de FILESTREAM almacenado en el sistema de archivos. El identificador se puede pasar a cualquiera de las API de Win32 siguientes: [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426) o [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427). Si pasa este identificador a cualquier otra API de Win32, se devuelve un error de ERROR_ACCESS_DENIED. El identificador se debe cerrar al pasarlo a la API Win32 [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428) antes de que la transacción se confirme o se revierta. Si no se puede cerrar el identificador, se producirán pérdidas de los recursos del lado servidor.  
  
 Todo el acceso al contenedor de datos FILESTREAM debe realizarse en una transacción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[tsql](../../includes/tsql-md.md)] También puede ejecutar instrucciones en la misma transacción. Esto permite mantener la coherencia entre los datos SQL y los datos de BLOB FILESTREAM.  
  
 Para acceder al FILESTREAM BLOB con Win32, la [autorización de Windows](../../relational-databases/security/choose-an-authentication-mode.md) debe estar habilitada.  
  
> [!IMPORTANT]  
>  Cuando el archivo se abre para acceso de escritura, el agente FILESTREAM posee la transacción. Hasta que la transacción se libera, solo se permite la E/S de archivos Win32. Para liberar la transacción, se debe cerrar el identificador de escritura.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HANDLE OpenSqlFilestream (  
    LPCWSTR FilestreamPath,  
    SQL_FILESTREAM_DESIRED_ACCESS DesiredAccess,  
    ULONG OpenOptions,  
    LPBYTE FilestreamTransactionContext,  
    SIZE_T FilestreamTransactionContextLength,  
    PLARGE_INTEGER AllocationSize);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *FilestreamPath*  
 [in] Es la ruta **nvarchar(max)** devuelta por la función [PathName](../../relational-databases/system-functions/pathname-transact-sql.md) . Se debe llamar a PathName desde el contexto de una cuenta que tenga los permisos SELECT o UPDATE de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la tabla y la columna FILESTREAM.  
  
 *DesiredAccess*  
 [in] Establece el modo utilizado para tener acceso a los datos de BLOB FILESTREAM. Este valor se pasa a la [función DeviceIoControl](https://go.microsoft.com/fwlink/?LinkId=105527).  
  
|Nombre|Value|Significado|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|Se pueden leer datos de este archivo.|  
|SQL_FILESTREAM_WRITE|1|En este archivo se pueden escribir datos.|  
|SQL_FILESTREAM_READWRITE|2|En este archivo se pueden escribir y leer datos.|  
  
> [!NOTE]  
>  Estos valores se definen en la enumeración SQL_FILESTREAM_DESIRED_ACCESS en sqlncli.h.  
  
 *OpenOptions*  
 [in] Los atributos y marcas de archivo. Este parámetro también puede incluir cualquier combinación de las marcas siguientes.  
  
|Marca|Value|Significado|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|El archivo se abre o se crea sin opciones especiales.|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|El archivo se abre o se crea para E/S asincrónica.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|El sistema abre el archivo sin utilizar el almacenamiento en caché del sistema.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|El sistema no escribe mediante una caché intermedia. La escritura va directamente al disco.|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|Se tiene acceso a un archivo de forma secuencial, desde el principio hasta el final. El sistema puede considerar que esto es una sugerencia para optimizar el almacenamiento en caché del archivo. Si una aplicación mueve el puntero de archivo para obtener acceso aleatorio, puede que no se produzca un almacenamiento en caché óptimo.|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|Se tiene acceso a un archivo de forma aleatoria. El sistema puede considerar que esto es una sugerencia para optimizar el almacenamiento en caché del archivo.|  
  
 *FilestreamTransactionContext*  
 [in] El valor devuelto por la función [GET_FILESTREAM_TRANSACTION_CONTEXT](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) .  
  
 *FilestreamTransactionContextLength*  
 [in] Número de bytes en los datos **varbinary(max)** devueltos por la función GET_FILESTREAM_TRANSACTION_CONTEXT. La función devuelve una matriz de N bytes. N viene determinada por la función y es una propiedad de la matriz de bytes devuelta.  
  
 *AllocationSize*  
 [in] Especifica el tamaño de asignación inicial del archivo de datos en bytes. Se pasa por alto en modo de lectura. Este parámetro puede ser NULL, en cuyo caso se utiliza el comportamiento predeterminado del sistema de archivos.  
  
## <a name="return-value"></a>Valor devuelto  
 Si la función se ejecuta correctamente, el valor devuelto es un identificador abierto para un archivo especificado. Si se produce un error en la función, el valor devuelto es INVALID_HANDLE_VALUE. Para obtener información de error extendida, llame a GetLastError().  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cómo utilizar la API `OpenSqlFilestream` para obtener un identificador Win32.  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/access-filestream-data-w_0_1.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/access-filestream-data-w_0_2.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/access-filestream-data-w_0_3.cpp)]  
  
## <a name="remarks"></a>Observaciones  
 Para utilizar esta API, debe estar instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se instala con las herramientas cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Instalar SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="see-also"></a>Consulte también  
 [Binary Large Object &#40;Blob&#41; Data &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [Realizar actualizaciones parciales de los datos FILESTREAM](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)   
 [Evitar conflictos con operaciones de base de datos en aplicaciones FILESTREAM](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
