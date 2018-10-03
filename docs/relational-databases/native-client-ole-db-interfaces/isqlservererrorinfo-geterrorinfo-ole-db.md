---
title: 'ISQLServerErrorInfo:: GetErrorInfo (OLE DB) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3c140e3891b5d1f5e73600a3cb623e5a0e8ce463
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606641"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Devuelve un puntero a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSERRORINFO del proveedor OLE DB de Native Client estructura que contenga la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detalles del error.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define la **ISQLServerErrorInfo** interfaz de errores. Esta interfaz devuelve los detalles de un error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluso la gravedad y el estado.  

  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ppSSErrorInfo*[out]  
 Un puntero a una estructura SSERRORINFO. Si el método produce un error o no hay información de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociada al error, el proveedor no asigna memoria y se asegura de que el argumento *ppSSErrorInfo* dé como resultado un puntero nulo.  
  
 *ppErrorStrings*[out]  
 Un puntero a una cadena de caracteres Unicode. Si el método produce un error o no hay información de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociada a un error, el proveedor no asigna memoria y se asegura de que el argumento *ppErrorStrings* dé como resultado un puntero nulo. Cuando se libera el argumento *ppErrorStrings* con el método **IMalloc::Free**, se liberan los tres miembros de cadena de la estructura SSERRORINFO devuelta, ya que la memoria se asigna en un bloque.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_INVALIDARG  
 Ya sea el *ppSSErrorInfo* o *ppErrorStrings* argumento era NULL.  
  
 E_OUTOFMEMORY  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no pudo asignar memoria suficiente para completar la solicitud.  
  
## <a name="remarks"></a>Comentarios  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client asigna memoria para las cadenas SSERRORINFO y OLECHAR devueltas a través de los punteros pasados por el consumidor. El consumidor debe desasignar esta memoria mediante el método **IMalloc::Free** cuando ya no requiera tener acceso a los datos de error.  
  
 La estructura SSERRORINFO se define como sigue:  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*pwszMessage*|El mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El mensaje se devuelve a través del método **IErrorInfo::GetDescription**.|  
|*pwszServer*|El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se ha producido el error.|  
|*pwszProcedure*|El nombre del procedimiento almacenado que genera el error si éste se produjo en un procedimiento almacenado; de lo contrario, una cadena vacía.|  
|*lNative*|El número de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El número de error es idéntico al devuelto en el parámetro *plNativeError* del método **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|El estado del error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|La gravedad del error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Cuando sea aplicable, la línea de un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que generó el mensaje de error. Si no hay implicado ningún procedimiento, se utiliza el valor predeterminado 1.|  
  
 Los punteros de las direcciones de referencia de la estructura en la cadena devuelta en el argumento *ppErrorStrings*.  
  
## <a name="see-also"></a>Vea también  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
