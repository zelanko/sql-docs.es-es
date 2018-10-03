---
title: Detalles del Error SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c7535e4579204834fc8024b7c37c46675320b8f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103945"
---
# <a name="sql-server-error-detail"></a>Detalles de errores de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define la interfaz de error específico del proveedor [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md). La interfaz devuelve más detalles acerca de un error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y resulta útil cuando se produce un error en la ejecución del comando o en operaciones de conjunto de filas.  
  
 Hay dos maneras de obtener acceso a la interfaz **ISQLServerErrorInfo**.  
  
 El consumidor puede llamar a **IErrorRecords::GetCustomerErrorObject** para obtener un puntero **ISQLServerErrorInfo**, tal como se muestra en el ejemplo de código siguiente. (No hay ninguna necesidad de obtener **ISQLErrorInfo**). **ISQLErrorInfo** e **ISQLServerErrorInfo** son objetos de error de OLE DB personalizados; **ISQLServerErrorInfo** es la interfaz que se usa para obtener información de errores de servidor, incluidos detalles como el nombre del procedimiento y los números de línea.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Otra manera de obtener un puntero **ISQLServerErrorInfo** consiste en llamar al método **QueryInterface** en un puntero **ISQLErrorInfo** ya obtenido. Tenga en cuenta que, como **ISQLServerErrorInfo** contiene un superconjunto de la información disponible en **ISQLErrorInfo**, conviene pasar directamente a **ISQLServerErrorInfo** a través de **GetCustomerErrorObject**.  
  
 La interfaz **ISQLServerErrorInfo** expone una función miembro, [ISQLServerErrorInfo::GetErrorInfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). La función devuelve un puntero a una estructura SSERRORINFO y un puntero a un búfer de cadena. Ambos punteros hacen referencia a la memoria que el consumidor debe desasignar mediante el método **IMalloc::Free**.  
  
 El consumidor interpreta los miembros de la estructura SSERRORINFO de la siguiente manera.  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*pwszMessage*|Mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Idéntico a la cadena que se devuelve en **IErrorInfo::GetDescription**.|  
|*pwszServer*|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la sesión.|  
|*pwszProcedure*|Si procede, nombre del procedimiento donde se ha producido el error. De lo contrario, una cadena vacía.|  
|*lNative*|Número del error nativo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Idéntico al valor que se devuelve en el parámetro *plNativeError* de **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|Estado de un mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|Gravedad de un mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Si procede, número de línea del procedimiento almacenado donde se produjo el error.|  
  
## <a name="see-also"></a>Vea también  
 [Errores](errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
