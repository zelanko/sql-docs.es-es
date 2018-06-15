---
title: Detalles del Error SQL Server | Documentos de Microsoft
description: Detalles del error de SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8b69559a6c89f30c73245633aa67db90ce7cd78a
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665585"
---
# <a name="sql-server-error-detail"></a>Detalles de errores de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server define la interfaz de error específico del proveedor [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1). La interfaz devuelve más detalles acerca de un error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y resulta útil cuando se produce un error en la ejecución del comando o en operaciones de conjunto de filas.  
  
 Hay dos maneras de obtener acceso a **ISQLServerErrorInfo** interfaz.  
  
 El consumidor puede llamar a **IErrorRecords:: Getcustomererrorobject** para obtener un **ISQLServerErrorInfo** puntero, como se muestra en el ejemplo de código siguiente. (No es necesario obtener **ISQLErrorInfo.**) Ambos **ISQLErrorInfo** y **ISQLServerErrorInfo** son objetos de error de OLE DB personalizados; **ISQLServerErrorInfo** es la interfaz que usa para obtener información de errores del servidor, incluidos detalles como los números de línea y de nombre de procedimiento.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Otra manera de obtener un **ISQLServerErrorInfo** puntero consiste en llamar a la **QueryInterface** método en una ya obtenido **ISQLErrorInfo** puntero. Tenga en cuenta que, dado que **ISQLServerErrorInfo** contiene un supraconjunto de la información disponible en **ISQLErrorInfo**, tiene sentido para ir directamente a **ISQLServerErrorInfo** a través de **GetCustomerErrorObject**.  
  
 El **ISQLServerErrorInfo** interfaz expone una función miembro, [ISQLServerErrorInfo:: GetErrorInfo](../../oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). La función devuelve un puntero a una estructura SSERRORINFO y un puntero a un búfer de cadena. Ambos punteros hacen referencia a memoria que el consumidor debe desasignar utilizando el **IMalloc:: Free** método.  
  
 El consumidor interpreta los miembros de la estructura SSERRORINFO de la siguiente manera.  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*pwszMessage*|Mensaje de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Idéntica a la cadena devuelta en **IErrorInfo:: GetDescription**.|  
|*pwszServer*|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la sesión.|  
|*pwszProcedure*|Si procede, nombre del procedimiento donde se ha producido el error. De lo contrario, una cadena vacía.|  
|*lNative*|Número del error nativo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Idéntico al valor devuelto en el *plNativeError* parámetro de **ISQLErrorInfo:: GetSQLInfo**.|  
|*bState*|Estado de un mensaje de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*bClass*|Gravedad de un mensaje de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Si procede, número de línea del procedimiento almacenado donde se produjo el error.|  
  
## <a name="see-also"></a>Vea también  
 [errores](../../oledb/ole-db-errors/errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
