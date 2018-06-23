---
title: 'Ibcpsession:: Bcpwritefmt (OLE DB) | Documentos de Microsoft'
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
- IBCPSession::BCPWriteFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3f7b2437a8a1a46b84f011eb631887d39f7c96eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106739"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
  Escribe la información de formato de cada columna en el archivo de formato.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPWriteFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Notas  
 El archivo de formato especifica el formato de los datos de un archivo de datos creado mediante copia masiva. Llamadas a la [ibcpsession:: BCPColumns](ibcpsession-bcpcolumns-ole-db.md) y [ibcpsession:: BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) los métodos definen el formato del archivo de datos. El método **BCPWriteFmt** guarda esta definición en el archivo al que se hace referencia en el argumento pwszFormatFile.  
  
 El método **BCPWriteFmt** puede guardar los archivos de formato en formato xml o de texto. Esto se debe indicar mediante la opción de control BCP_OPTION_XML con el [ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md) método.  
  
 Para cargar un archivo de formato guardado, utilice la [ibcpsession:: Bcpreadfmt](ibcpsession-bcpreadfmt-ole-db.md) método.  
  
## <a name="arguments"></a>Argumentos  
 *pwszFormatFile*[in]  
 La ruta de acceso y nombre del archivo que contiene los valores de formato para el archivo de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor; Para obtener información detallada, use la [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) interfaz.  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, el [ibcpsession:: BCPInit](ibcpsession-bcpinit-ole-db.md) no se llamó el método antes de llamar a este método.  
  
## <a name="see-also"></a>Vea también  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../native-client/features/performing-bulk-copy-operations.md)  
  
  