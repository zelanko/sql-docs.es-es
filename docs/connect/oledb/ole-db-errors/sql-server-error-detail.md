---
title: Detalles del Error SQL Server | Microsoft Docs
description: Detalle del error de SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: aa151a9cf85d2ddf131a530d09d884c6fd7bbca4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66791591"
---
# <a name="sql-server-error-detail"></a>Detalles de errores de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server define la interfaz de error específico del proveedor [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1). La interfaz devuelve más detalles acerca de un error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y resulta útil cuando se produce un error en la ejecución del comando o en operaciones de conjunto de filas.  
  
 Hay dos maneras de obtener acceso a la interfaz **ISQLServerErrorInfo**.  
  
 El consumidor puede llamar a **IErrorRecords::GetCustomerErrorObject** para obtener un puntero **ISQLServerErrorInfo**, tal como se muestra en el ejemplo de código siguiente. (No hay ninguna necesidad de obtener **ISQLErrorInfo**). **ISQLErrorInfo** e **ISQLServerErrorInfo** son objetos de error de OLE DB personalizados; **ISQLServerErrorInfo** es la interfaz que se usa para obtener información de errores de servidor, incluidos detalles como el nombre del procedimiento y los números de línea.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Otra manera de obtener un puntero **ISQLServerErrorInfo** consiste en llamar al método **QueryInterface** en un puntero **ISQLErrorInfo** ya obtenido. Tenga en cuenta que, como **ISQLServerErrorInfo** contiene un superconjunto de la información disponible en **ISQLErrorInfo**, conviene pasar directamente a **ISQLServerErrorInfo** a través de **GetCustomerErrorObject**.  
  
 La interfaz **ISQLServerErrorInfo** expone una función miembro, [ISQLServerErrorInfo::GetErrorInfo](../../oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). La función devuelve un puntero a una estructura SSERRORINFO y un puntero a un búfer de cadena. Ambos punteros hacen referencia a la memoria que el consumidor debe desasignar mediante el método **IMalloc::Free**.  
  
 El consumidor interpreta los miembros de la estructura SSERRORINFO de la siguiente manera.  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*pwszMessage*|Mensaje de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Idéntico a la cadena que se devuelve en **IErrorInfo::GetDescription**.|  
|*pwszServer*|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la sesión.|  
|*pwszProcedure*|Si procede, nombre del procedimiento donde se ha producido el error. De lo contrario, una cadena vacía.|  
|*lNative*|Número del error nativo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Idéntico al valor que se devuelve en el parámetro *plNativeError* de **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|Estado de un mensaje de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*bClass*|Gravedad de un mensaje de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Si procede, número de línea del procedimiento almacenado donde se produjo el error.|  
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../oledb/ole-db-errors/errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
