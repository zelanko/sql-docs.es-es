---
description: 'IBCPSession:: BCPExec (proveedor de OLE DB de Native Client)'
title: 'IBCPSession:: BCPExec (proveedor de OLE DB de Native Client) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IBCPSession::BCPExec (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPExec method
ms.assetid: 0f4ebb63-cf03-4e53-846e-6c3021cde007
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6163580d55bf4a1e0a04067328ef293d07688bce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486885"
---
# <a name="ibcpsessionbcpexec-native-client-ole-db-provider"></a>IBCPSession:: BCPExec (proveedor de OLE DB de Native Client)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Realiza la operación de copia masiva.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPExec(   
      DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>Observaciones  
 El método **BCPExec** copia los datos de un archivo de usuario en una tabla de base de datos o viceversa, en función del valor del parámetro *eDirection* usado con el método [IBCPSession::BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md).  
  
 Antes de llamar a **BCPExec**, llame al método **BCPInit** con un nombre de archivo de usuario válido. Si no lo hace, se producirá un error. La única excepción es que una consulta vaya a utilizarse para una operación de salida de copia masiva. En ese caso, especifique NULL para el nombre de tabla en el método **BCPInit** y, a continuación, especifique la consulta mediante la opción BCP_OPTION_HINTS.  
  
 El método **BCPExec** es el único método de copia masiva que es probable que quede pendiente durante un período de tiempo indeterminado. Por lo tanto, es el único método de copia masiva que admite el modo asincrónico. Para usar el modo asincrónico, establezca la propiedad de sesión SSPROP_ASYNCH_BULKCOPY específica del proveedor en VARIANT_TRUE antes de llamar al método **BCPExec** . Esta propiedad se encuentra disponible en el conjunto de propiedades DBPROPSET_SQLSERVERSESSION. Para comprobar si se ha completado, llame al método **BCPExec** con los mismos parámetros. Si la copia masiva aún no se ha completado, el método **BCPExec** devuelve DB_S_ASYNCHRONOUS. También devuelve en el argumento *pRowsCopied* un recuento de estado del número de filas que se han enviado al servidor o que se han recibido del servidor. Las filas enviadas al servidor no se confirman hasta que se alcanza el final de un lote.  
  
## <a name="arguments"></a>Argumentos  
 *pRowsCopied*[out]  
 Puntero a un valor de tipo DWORD. El método **BCPExec** rellena el valor DWORD con el número de filas que se han copiado correctamente. Si el argumento *pRowsCopied* está establecido en NULL, el método **BCPExec** lo omite.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor; para obtener información detallada, use la interfaz [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15).  
  
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
  
## <a name="see-also"></a>Consulte también  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
