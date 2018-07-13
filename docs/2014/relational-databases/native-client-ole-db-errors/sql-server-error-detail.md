---
title: Detalles del Error SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b937fda454ae08549917cdf3682ef20c76373a6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408994"
---
# <a name="sql-server-error-detail"></a>Detalles de errores de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define la interfaz de error específico del proveedor [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md). La interfaz devuelve más detalles acerca de un error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y resulta útil cuando se produce un error en la ejecución del comando o en operaciones de conjunto de filas.  
  
 Hay dos maneras de obtener acceso a **ISQLServerErrorInfo** interfaz.  
  
 El consumidor puede llamar a **IErrorRecords:: Getcustomererrorobject** para obtener un **ISQLServerErrorInfo** puntero, como se muestra en el siguiente ejemplo de código. (No es necesario obtener **ISQLErrorInfo.**) Ambos **ISQLErrorInfo** y **ISQLServerErrorInfo** son objetos de error de OLE DB personalizados; **ISQLServerErrorInfo** que se va a utilizar para obtener información de la interfaz de errores del servidor, incluidos detalles como los números de línea y de nombre de procedimiento.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Otra forma de obtener un **ISQLServerErrorInfo** puntero es llamar a la **QueryInterface** método en una ya obtenido **ISQLErrorInfo** puntero. Tenga en cuenta que dado que **ISQLServerErrorInfo** contiene un superconjunto de la información disponible en **ISQLErrorInfo**, tiene sentido para ir directamente a **ISQLServerErrorInfo**a través de **GetCustomerErrorObject**.  
  
 El **ISQLServerErrorInfo** interfaz expone una función miembro, [ISQLServerErrorInfo:: GetErrorInfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). La función devuelve un puntero a una estructura SSERRORINFO y un puntero a un búfer de cadena. Ambos punteros hacen referencia a memoria que el consumidor debe desasignar utilizando el **IMalloc:: Free** método.  
  
 El consumidor interpreta los miembros de la estructura SSERRORINFO de la siguiente manera.  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*pwszMessage*|Mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Idéntica a la cadena devuelta en **IErrorInfo:: GetDescription**.|  
|*pwszServer*|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la sesión.|  
|*pwszProcedure*|Si procede, nombre del procedimiento donde se ha producido el error. De lo contrario, una cadena vacía.|  
|*lNative*|Número del error nativo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Idéntico al valor devuelto en el *plNativeError* parámetro de **ISQLErrorInfo:: GetSQLInfo**.|  
|*bState*|Estado de un mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|Gravedad de un mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Si procede, número de línea del procedimiento almacenado donde se produjo el error.|  
  
## <a name="see-also"></a>Vea también  
 [Errores](errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
