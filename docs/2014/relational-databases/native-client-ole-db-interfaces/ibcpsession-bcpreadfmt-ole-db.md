---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) | Documentos de Microsoft'
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
- IBCPSession::BCPReadFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPReadFmt method
ms.assetid: e2a12050-94e4-48a3-8a48-b780d646f116
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f47369cb66f6695ca7a235beb72536ce34495bb5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204395"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
  Lee la información de formato de cada columna en el archivo de formato.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPReadFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Notas  
 El método **BCPReadFmt** se utiliza para leer datos de un archivo de formato que especifica el formato de datos en el archivo de datos. Este método es capaz de detectar la versión correcta del archivo de formato. Puede detectar automáticamente si el archivo de formato está en xml o en el formato de texto de estilo anterior y se comporta en consecuencia. Las versiones de archivo de formato admitidas por la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client BCP son de la versión 6.0 o posterior.  
  
 Después de la **BCPReadFmt** método lee los valores de formato, realiza las llamadas adecuadas a la [ibcpsession:: BCPColumns](ibcpsession-bcpcolumns-ole-db.md) y [ibcpsession:: BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) métodos. No es necesario que analice un archivo de formato y realice estas llamadas.  
  
 Para guardar un archivo de formato, llame a la [ibcpsession:: Bcpwritefmt](ibcpsession-bcpwritefmt-ole-db.md) método. Las llamadas al método **BCPReadFmt** pueden hacer referencia a formatos guardados. Como alternativa, la utilidad de copia masiva (**bcp**) puede guardar formatos de datos definidos por el usuario en archivos a los que puede hacer referencia el método **BCPReadFmt** .  
  
 El `BCP_OPTION_DELAYREADFMT` valor de la *eOption* parámetro de [ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md) modifica el comportamiento de ibcpsession:: Bcpreadfmt.  
  
## <a name="arguments"></a>Argumentos  
 *pwszFormatFile*[in]  
 La ruta de acceso y nombre del archivo que contiene los valores de formato para el archivo de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor, para obtener información detallada, use la [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) interfaz.  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, el [ibcpsession:: BCPInit](ibcpsession-bcpinit-ole-db.md) no se llamó el método antes de llamar a este método.  
  
## <a name="see-also"></a>Vea también  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../native-client/features/performing-bulk-copy-operations.md)  
  
  