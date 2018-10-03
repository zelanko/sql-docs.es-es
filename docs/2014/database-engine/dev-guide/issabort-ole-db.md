---
title: ISSAbort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a4b3e43dca5a18a991733492eeeffc4f49d14ef8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48181245"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  El **ISSAbort** interfaz, que se expone en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, proporciona el [issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) método que se utiliza para cancelar el conjunto de filas actual más los comandos por lotes el comando que inicialmente generó el conjunto de filas, y que todavía no han completado la ejecución.  
  
 **ISSAbort** es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaz específica del proveedor de cliente nativo disponible mediante el uso de **QueryInterface** en el **IMultipleResults** objeto devuelto por  **ICommand:: Execute** o **IOpenRowset:: OpenRowset**.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Descripción|  
|------------|-----------------|  
|[Issabort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|Cancela el conjunto de filas actual y los comandos en lotes asociados al comando actual.|  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
