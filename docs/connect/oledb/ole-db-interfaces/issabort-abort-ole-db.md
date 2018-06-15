---
title: 'Issabort:: Abort (OLE DB) | Documentos de Microsoft'
description: ISSAbort::Abort (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0c7d30e8132d245958e7ef6f7f09e642a2da960c
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305384"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cancela el conjunto de filas actual y los comandos en lotes asociados al comando actual.  
  
El **ISSAbort** interfaz, que se expone en el controlador OLE DB para SQL Server, proporciona el **issabort:: Abort** método que se utiliza para cancelar el conjunto de filas actual más los comandos por lotes con el comando que inicialmente generó el conjunto de filas, y que aún no se han completado la ejecución.  
  
 **ISSAbort** está disponible un controlador OLE DB para la interfaz específica de SQL Server usando **QueryInterface** en el **IMultipleResults** objeto devuelto por **ICommand:: Execute**  o **IOpenRowset:: OpenRowset**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Notas  
 Si el comando que se va a anular está en un procedimiento almacenado, se terminará la ejecución del procedimiento almacenado (y los procedimientos, que haya llamado a ese procedimiento), así como el lote de comandos que contiene la llamada al procedimiento almacenado. Si el servidor está realizando la transferencia de un conjunto de resultados para el cliente, se detendrá la transferencia. Si el cliente no desea consumir un conjunto de resultados, la llamada a **ISSAbort::Abort** antes de liberar el conjunto de filas acelerará la liberación del conjunto de filas, pero si hay una transacción abierta y XACT_ABORT está establecido en ON, la transacción se revertirá al llamar a **ISSAbort::Abort** .  
  
 Después de **issabort:: Abort** devuelve S_OK, asociado **IMultipleResults** interfaz entra en un estado inutilizable y devuelve DB_E_CANCELED a todas las llamadas de método (excepto en los métodos definidos por el **IUnknown** interfaz) hasta que se libera. Si se ha obtenido una interfaz **IRowset** de **IMultipleResults** antes de una llamada a **Anular**, también inicia un estado inutilizable y devuelve DB_E_CANCELED a todas las llamadas a método (excepto en los métodos que define la interfaz **IUNKNOWN** e **IRowset::ReleaseRows**) hasta que se libera después de una llamada correcta a **ISSAbort::Abort**.  
  
> [!NOTE]  
>  A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], si el estado de servidor XACT_ABORT es ON, ejecutar **issabort:: Abort** finalizará y revertir una transacción implícita o explícita actual cuando se conecta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no anularán la transacción actual.  
  
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
 Se produjo un error específico del proveedor; Para obtener información detallada, use la [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interfaz.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, el objeto está en un estado zombi porque ya se ha llamado a **ISSAbort::Abort** .  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
  
