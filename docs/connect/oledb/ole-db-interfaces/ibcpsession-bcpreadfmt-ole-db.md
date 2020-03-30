---
title: IBCPSession::BCPReadFmt (OLE DB) | Microsoft Docs
description: Uso de IBCPSession::BCPReadFmt para leer datos de un archivo de formato (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 97274315275f11e77c458827740f44906a524ed9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015499"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Lee la información de formato de cada columna en el archivo de formato.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Observaciones  
 El método **BCPReadFmt** se utiliza para leer datos de un archivo de formato que especifica el formato de datos en el archivo de datos. Este método es capaz de detectar la versión correcta del archivo de formato. Puede detectar automáticamente si el archivo de formato está en xml o en el formato de texto de estilo anterior y se comporta en consecuencia. Las versiones del archivo de formato admitidas por el BCP de OLE DB Driver for SQL Server son la 6.0 o más reciente.  
  
 Después de que el método **BCPReadFmt** lee los valores de formato, realiza las llamadas adecuadas a los métodos [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) e [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md). No es necesario que analice un archivo de formato y realice estas llamadas.  
  
 Para guardar un archivo de formato, llame al método [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md). Las llamadas al método **BCPReadFmt** pueden hacer referencia a formatos guardados. Como alternativa, la utilidad de copia masiva (**bcp**) puede guardar formatos de datos definidos por el usuario en archivos a los que puede hacer referencia el método **BCPReadFmt** .  
  
 El valor **BCP_OPTION_DELAYREADFMT** del parámetro *eOption* de [IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) modifica el comportamiento de IBCPSession::BCPReadFmt.  
  
## <a name="arguments"></a>Argumentos  
 *pwszFormatFile*[in]  
 La ruta de acceso y nombre del archivo que contiene los valores de formato para el archivo de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor; para obtener información detallada, use la interfaz [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, no se llamó al método [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) antes de llamar a este método.  
  
## <a name="see-also"></a>Consulte también  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
