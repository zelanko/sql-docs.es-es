---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) | Documentos de Microsoft'
description: 'Utilizando ibcpsession:: Bcpreadfmt para leer los datos desde un archivo de formato (OLE DB)'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: dd4bd2bc59d7861c228941a946b3eaed576f2efb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Lee la información de formato de cada columna en el archivo de formato.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Comentarios  
 El método **BCPReadFmt** se utiliza para leer datos de un archivo de formato que especifica el formato de datos en el archivo de datos. Este método es capaz de detectar la versión correcta del archivo de formato. Puede detectar automáticamente si el archivo de formato está en xml o en el formato de texto de estilo anterior y se comporta en consecuencia. Las versiones de archivo de formato admitidas por el controlador OLE DB para BCP de SQL Server son de la versión 6.0 o posterior.  
  
 Después de la **BCPReadFmt** método lee los valores de formato, realiza las llamadas adecuadas a la [ibcpsession:: BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) y [ibcpsession:: BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) métodos. No es necesario que analice un archivo de formato y realice estas llamadas.  
  
 Para guardar un archivo de formato, llame a la [ibcpsession:: Bcpwritefmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) método. Las llamadas al método **BCPReadFmt** pueden hacer referencia a formatos guardados. Como alternativa, la utilidad de copia masiva (**bcp**) puede guardar formatos de datos definidos por el usuario en archivos a los que puede hacer referencia el método **BCPReadFmt** .  
  
 El **BCP_OPTION_DELAYREADFMT** valor de la *eOption* parámetro de [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) modifica el comportamiento de ibcpsession:: Bcpreadfmt.  
  
## <a name="arguments"></a>Argumentos  
 *pwszFormatFile*[in]  
 La ruta de acceso y nombre del archivo que contiene los valores de formato para el archivo de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor, para obtener información detallada, use la [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interfaz.  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, el [ibcpsession:: BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) no se llamó el método antes de llamar a este método.  
  
## <a name="see-also"></a>Vea también  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
