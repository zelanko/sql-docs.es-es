---
title: 'ISQLServerErrorInfo:: GetErrorInfo (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f33c66d8e521339573e56b78407f0bab67b4b43e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430104"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
  Devuelve un puntero a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSERRORINFO del proveedor OLE DB de Native Client estructura que contenga la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detalles del error.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
   HRESULT GetErrorInfo(  
SSERRORINFO**ppSSErrorInfo,  
OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ppSSErrorInfo*[out]  
 Un puntero a una estructura SSERRORINFO. Si se produce un error en el método o no hay ningún [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información asociada con el error, el proveedor no asigna memoria y se asegura de que el *ppSSErrorInfo* argumento es un puntero nulo en la salida.  
  
 *ppErrorStrings*[out]  
 Un puntero a una cadena de caracteres Unicode. Si se produce un error en el método o no hay ningún [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información asociada a un error, el proveedor no asigna memoria y se asegura de que el *ppErrorStrings* argumento es un puntero nulo en la salida. Liberar la *ppErrorStrings* argumento con el **IMalloc:: Free** método libera los tres miembros de la cadena de la estructura SSERRORINFO devuelta, tal como se asigna la memoria en un bloque.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_INVALIDARG  
 Ya sea el *ppSSErrorInfo* o *ppErrorStrings* argumento era NULL.  
  
 E_OUTOFMEMORY  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no pudo asignar memoria suficiente para completar la solicitud.  
  
## <a name="remarks"></a>Notas  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client asigna memoria para las cadenas SSERRORINFO y OLECHAR devueltas a través de los punteros pasados por el consumidor. El consumidor debe desasignar esta memoria utilizando la **IMalloc:: Free** método cuando ya no requiere acceso a los datos de error.  
  
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
|*pwszMessage*|El mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se devuelve el mensaje a través de la **IErrorInfo:: GetDescription** método.|  
|*pwszServer*|El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se ha producido el error.|  
|*pwszProcedure*|El nombre del procedimiento almacenado que genera el error si éste se produjo en un procedimiento almacenado; de lo contrario, una cadena vacía.|  
|*lNative*|El número de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El número de error es idéntico al devuelto en el *plNativeError* parámetro de la **ISQLErrorInfo:: GetSQLInfo** método.|  
|*bState*|El estado del error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|La gravedad del error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Cuando sea aplicable, la línea de un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que generó el mensaje de error. Si no hay implicado ningún procedimiento, se utiliza el valor predeterminado 1.|  
  
 En la estructura de los punteros hacen referencia a direcciones en la cadena devuelta en el *ppErrorStrings* argumento.  
  
## <a name="see-also"></a>Vea también  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
