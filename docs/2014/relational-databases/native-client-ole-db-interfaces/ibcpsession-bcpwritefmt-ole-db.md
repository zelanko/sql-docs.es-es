---
title: IBCPSession::BCPWriteFmt (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPWriteFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
author: rothja
ms.author: jroth
ms.openlocfilehash: ec126f82b3bae86701f2723bb8b93180916dc6b6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047954"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
  Escribe la información de formato de cada columna en el archivo de formato.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPWriteFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Comentarios  
 El archivo de formato especifica el formato de los datos de un archivo de datos creado mediante copia masiva. Las llamadas a los métodos [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) e [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) definen el formato del archivo de datos. El método **BCPWriteFmt** guarda esta definición en el archivo al que se hace referencia en el argumento pwszFormatFile.  
  
 El método **BCPWriteFmt** puede guardar los archivos de formato en formato xml o de texto. Esto se debe indicar mediante la opción de control BCP_OPTION_XML con el método [IBCPSession::BCPControl](ibcpsession-bcpcontrol-ole-db.md).  
  
 Para cargar un archivo de formato guardado, use el método [IBCPSession::BCPReadFmt](ibcpsession-bcpreadfmt-ole-db.md).  
  
## <a name="arguments"></a>Argumentos  
 *pwszFormatFile*[in]  
 La ruta de acceso y nombre del archivo que contiene los valores de formato para el archivo de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor. para obtener información detallada, use la interfaz [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) .  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, no se llamó al método [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) antes de llamar a este método.  
  
## <a name="see-also"></a>Consulte también  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../native-client/features/performing-bulk-copy-operations.md)  
  
  
