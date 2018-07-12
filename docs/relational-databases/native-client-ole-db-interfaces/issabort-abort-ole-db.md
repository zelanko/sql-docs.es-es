---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 90fdb17506d624e5210288716736ae29721c0feb
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431264"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Cancela el conjunto de filas actual y los comandos en lotes asociados al comando actual.  
  
El **ISSAbort** interfaz, que se expone en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, proporciona el **issabort:: Abort** método que se utiliza para cancelar el conjunto de filas actual más los comandos por lotes el comando que inicialmente generó el conjunto de filas, y que todavía no han completado la ejecución.  
  
 **ISSAbort** es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaz específica del proveedor de cliente nativo disponible mediante el uso de **QueryInterface** en el **IMultipleResults** objeto devuelto por  **ICommand:: Execute** o **IOpenRowset:: OpenRowset**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Notas  
 Si el comando que se anula se encuentra en un procedimiento almacenado, terminará la ejecución del procedimiento almacenado (y cualquier procedimiento que haya llamado a este procedimiento) así como del lote de comandos que contiene la llamada al procedimiento almacenado. Si el servidor está en proceso de transferir un conjunto de resultados al cliente, se detendrá. Si el cliente no desea consumir un conjunto de resultados, la llamada a **ISSAbort::Abort** antes de liberar el conjunto de filas acelerará la liberación del conjunto de filas, pero si hay una transacción abierta y XACT_ABORT está establecido en ON, la transacción se revertirá al llamar a **ISSAbort::Abort** .  
  
 Después de que **ISSAbort::Abort** devuelva S_OK, la interfaz **IMultipleResults** asociada inicia un estado inutilizable y devuelve DB_E_CANCELED a todas las llamadas a método (excepto en los métodos que define la interfaz **IUNKNOWN** ) hasta que se libera. Si se ha obtenido una interfaz **IRowset** de **IMultipleResults** antes de una llamada a **Anular**, también inicia un estado inutilizable y devuelve DB_E_CANCELED a todas las llamadas a método (excepto en los métodos que define la interfaz **IUNKNOWN** e **IRowset::ReleaseRows**) hasta que se libera después de una llamada correcta a **ISSAbort::Abort**.  
  
> [!NOTE]  
>  A partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], si el servidor de estado XACT_ABORT está establecido en, la ejecución **issabort:: Abort** finalizará y revertirá cualquier transacción implícita o explícita actual cuando se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no anularán la transacción actual.  
  
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
 Se produjo un error específico del proveedor; Para obtener información detallada, use el [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interfaz.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, el objeto está en un estado zombi porque ya se ha llamado a **ISSAbort::Abort** .  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
## <a name="see-also"></a>Vea también  
 [ISSAbort &#40;OLE DB&#41;](http://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
