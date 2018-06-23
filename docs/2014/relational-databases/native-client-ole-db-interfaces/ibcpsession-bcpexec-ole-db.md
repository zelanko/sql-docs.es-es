---
title: Ibcpsession (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IBCPSession::BCPExec (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPExec method
ms.assetid: 0f4ebb63-cf03-4e53-846e-6c3021cde007
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 262593c696579352a1e369b369f8001e551d66be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199352"
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec (OLE DB)
  Realiza la operación de copia masiva.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPExec(   
DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>Notas  
 El **BCPExec** método copia los datos de un archivo de usuario a una tabla de base de datos o viceversa, dependiendo del valor de la *eDirection* parámetro utilizado con el [ibcpsession:: BCPInit](ibcpsession-bcpinit-ole-db.md)(método).  
  
 Antes de llamar a **BCPExec**, llame al método **BCPInit** con un nombre de archivo de usuario válido. Si no lo hace, se producirá un error. La única excepción es que una consulta vaya a utilizarse para una operación de salida de copia masiva. En ese caso, especifique NULL para el nombre de tabla en el método **BCPInit** y, a continuación, especifique la consulta mediante la opción BCP_OPTION_HINTS.  
  
 El método **BCPExec** es el único método de copia masiva que es probable que quede pendiente durante un período de tiempo indeterminado. Por lo tanto, es el único método de copia masiva que admite el modo asincrónico. Para usar el modo asincrónico, establezca la propiedad de sesión SSPROP_ASYNCH_BULKCOPY específica del proveedor en VARIANT_TRUE antes de llamar al método **BCPExec** . Esta propiedad se encuentra disponible en el conjunto de propiedades DBPROPSET_SQLSERVERSESSION. Para comprobar si se ha completado, llame al método **BCPExec** con los mismos parámetros. Si la copia masiva aún no se ha completado, el método **BCPExec** devuelve DB_S_ASYNCHRONOUS. También devuelve en el argumento *pRowsCopied* un recuento de estado del número de filas que se han enviado al servidor o que se han recibido del servidor. Las filas enviadas al servidor no se confirman hasta que se alcanza el final de un lote.  
  
## <a name="arguments"></a>Argumentos  
 *pRowsCopied*[out]  
 Puntero a un valor de tipo DWORD. El método **BCPExec** rellena el valor DWORD con el número de filas que se han copiado correctamente. Si el argumento *pRowsCopied* está establecido en NULL, el método **BCPExec** lo omite.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor; Para obtener información detallada, use la [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) interfaz.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, no se llamó al método **BCPInit** antes de llamar a este método. También se produce si la operación se anuló mediante el uso de la opción BCP_OPTION_ABORT y después se llamó al método **BCPExec** .  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
 DB_S_ENDOFROWSET  
 La operación de copia masiva finalizó y se completó toda la operación de transferencia de datos.  
  
 DB_S_ASYNCHRONOUS  
 Se copió el lote actual de filas. Vuelva a llamar al método **BCPExec** para transferir el siguiente lote.  
  
 DB_S_ERRORSOCCURRED  
 Se produjeron errores durante la operación de copia masiva y algunas filas no pudieron copiarse. El número de errores sigue siendo menor al número máximo de errores permitidos.  
  
## <a name="see-also"></a>Vea también  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../native-client/features/performing-bulk-copy-operations.md)  
  
  