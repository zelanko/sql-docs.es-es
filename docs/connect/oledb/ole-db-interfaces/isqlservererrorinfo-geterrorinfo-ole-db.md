---
title: ISQLServerErrorInfo::GetErrorInfo (controlador OLE DB) | Microsoft Docs
description: Obtenga información sobre cómo el método ISQLServerErrorInfo::GetErrorInfo devuelve un puntero a una estructura SSERRORINFO de OLE DB Driver for SQL Server con detalles de error de SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6c025b5832299867be8b611756b5e15d54109c2
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860087"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Devuelve un puntero a una estructura SSERRORINFO de OLE DB Driver for SQL Server que contiene los detalles del error [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 OLE DB Driver for SQL Server define la interfaz de errores **ISQLServerErrorInfo**. Esta interfaz devuelve los detalles de un error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], incluso la gravedad y el estado.  

  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ppSSErrorInfo*[out]  
 Un puntero a una estructura SSERRORINFO. Si el método produce un error o no hay información de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asociada al error, el proveedor no asigna memoria y se asegura de que el argumento *ppSSErrorInfo* dé como resultado un puntero nulo.  
  
 *ppErrorStrings*[out]  
 Un puntero a una cadena de caracteres Unicode. Si el método produce un error o no hay información de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asociada a un error, el proveedor no asigna memoria y se asegura de que el argumento *ppErrorStrings* dé como resultado un puntero nulo. Cuando se libera el argumento *ppErrorStrings* con el método **IMalloc::Free**, se liberan los tres miembros de cadena de la estructura SSERRORINFO devuelta, ya que la memoria se asigna en un bloque.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_INVALIDARG  
 El argumento *ppSSErrorInfo* o *ppErrorStrings* era NULL.  
  
 E_OUTOFMEMORY  
 OLE DB Driver for SQL Server no pudo asignar memoria suficiente para completar la solicitud.  
  
## <a name="remarks"></a>Observaciones  
 El controlador OLE DB para SQL Server asigna memoria para las cadenas SSERRORINFO y OLECHAR devueltas a través de los punteros pasados por el consumidor. El consumidor debe desasignar esta memoria mediante el método **IMalloc::Free** cuando ya no requiera tener acceso a los datos de error.  
  
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
  
|Member|Descripción|  
|------------|-----------------|  
|*pwszMessage*|El mensaje de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El mensaje se devuelve a través del método **IErrorInfo::GetDescription**.|  
|*pwszServer*|El nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que se ha producido el error.|  
|*pwszProcedure*|El nombre del procedimiento almacenado que genera el error si éste se produjo en un procedimiento almacenado; de lo contrario, una cadena vacía.|  
|*lNative*|El número de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El número de error es idéntico al devuelto en el parámetro *plNativeError* del método **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|El estado del error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*bClass*|La gravedad del error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Cuando sea aplicable, la línea de un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que generó el mensaje de error. Si no hay implicado ningún procedimiento, se utiliza el valor predeterminado 1.|  
  
 Los punteros de las direcciones de referencia de la estructura en la cadena devuelta en el argumento *ppErrorStrings*.  
  
## <a name="see-also"></a>Consulte también  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15)   
 [RAISERROR &#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
