---
title: ISSAbort (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 53c6e2c7c06331ce75883f86a8935d4d1c2419c4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108149"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  El **ISSAbort** interfaz, que se expone en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, proporciona el [issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) método que se utiliza para cancelar el conjunto de filas actual más los comandos por lotes con el comando que inicialmente generó el conjunto de filas, y que aún no se han completado la ejecución.  
  
 **ISSAbort** es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaz específica del proveedor de Native Client disponible mediante el uso de **QueryInterface** en el **IMultipleResults** objeto devuelto por  **ICommand:: Execute** o **IOpenRowset:: OpenRowset**.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Descripción|  
|------------|-----------------|  
|[Issabort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|Cancela el conjunto de filas actual y los comandos en lotes asociados al comando actual.|  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  