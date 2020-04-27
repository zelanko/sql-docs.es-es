---
title: ISSAbort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 801eb84df08837ec8e49b6bb0e28fc1f1115e674
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62781041"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  La interfaz **ISSAbort** , que se expone en el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, proporciona el método [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) que se utiliza para cancelar el conjunto de filas actual más los comandos incluidos en el mismo lote que el comando que inicialmente generó el conjunto de filas y que todavía no han completado la ejecución.  
  
 **ISSAbort** es una interfaz específica del proveedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Native Client que está disponible cuando se utiliza **QueryInterface** en el objeto **IMultipleResults** devuelto por **ICommand::Execute** o **IOpenRowset::OpenRowset**.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Descripción|  
|------------|-----------------|  
|[ISSAbort:: ABORT &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|Cancela el conjunto de filas actual y los comandos en lotes asociados al comando actual.|  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
