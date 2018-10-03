---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
description: ISSAbort::Abort (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 83d071404eb00d366e4da6966b921dcefd6e6579
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604904"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Cancela el conjunto de filas actual y los comandos en lotes asociados al comando actual.  
  
La interfaz **ISSAbort**, que se expone en el controlador OLE DB para SQL Server, proporciona el método **ISSAbort::Abort** que se usa para cancelar el conjunto de filas actual más los comandos incluidos en el mismo lote que el comando que inicialmente generó el conjunto de filas y que todavía no han completado la ejecución.  
  
 **ISSAbort** es una interfaz específica del controlador OLE DB para SQL Server que está disponible cuando se usa **QueryInterface** en el objeto **IMultipleResults** devuelto por **ICommand::Execute** o **IOpenRowset::OpenRowset**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Notas  
 Si el comando que se anula se encuentra en un procedimiento almacenado, finalizará la ejecución del procedimiento almacenado (y cualquier procedimiento que haya llamado a ese procedimiento) así como del lote de comandos que contiene la llamada al procedimiento almacenado. Si el servidor está en proceso de transferir un conjunto de resultados al cliente, se detendrá la transferencia. Si el cliente no desea consumir un conjunto de resultados, la llamada a **ISSAbort::Abort** antes de liberar el conjunto de filas acelerará la liberación del conjunto de filas, pero si hay una transacción abierta y XACT_ABORT está establecido en ON, la transacción se revertirá al llamar a **ISSAbort::Abort** .  
  
 Después de que **ISSAbort::Abort** devuelva S_OK, la interfaz **IMultipleResults** asociada inicia un estado inutilizable y devuelve DB_E_CANCELED a todas las llamadas a método (excepto en los métodos que define la interfaz **IUNKNOWN**) hasta que se libera. Si se ha obtenido una interfaz **IRowset** de **IMultipleResults** antes de una llamada a **Anular**, también inicia un estado inutilizable y devuelve DB_E_CANCELED a todas las llamadas a método (excepto en los métodos que define la interfaz **IUNKNOWN** e **IRowset::ReleaseRows**) hasta que se libera después de una llamada correcta a **ISSAbort::Abort**.  
  
> [!NOTE]  
>  A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], si el estado de servidor XACT_ABORT está establecido en ON, la ejecución de **ISSAbort::Abort** finalizará y revertirá cualquier transacción implícita o explícita actual al conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no anularán la transacción actual.  
  
## <a name="arguments"></a>Argumentos  
 Ninguno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método **ISSAbort::Abort** devuelve S_OK si el lote se ha cancelado y DB_E_CANTCANCEL de lo contrario. Si el lote ya se había cancelado, se devuelve DB_E_CANCELED.  
  
 DB_E_CANCELED  
 El lote ya se ha cancelado.  
  
 DB_E_CANTCANCEL  
 El lote no se ha cancelado.  
  
 E_FAIL  
 Se produjo un error específico del proveedor; para obtener información detallada, use la interfaz [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, el objeto está en un estado zombi porque ya se ha llamado a **ISSAbort::Abort** .  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
  
