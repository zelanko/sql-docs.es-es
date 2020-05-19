---
title: Comparabilidad de IRowsetFind | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability [ODBC]
ms.assetid: 7d148b56-9bbe-4e55-b31f-43f115705402
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 46391974a8c1a3b9e915330b3ce86d86f005aea7
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705072"
---
# <a name="comparability-for-irowsetfind"></a>Comparaciones en IRowsetFind
  IRowsetFind admite las comparaciones siguientes para los tipos de fecha y hora únicamente:  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 Si se intenta realizar cualquier otra comparación, se obtiene DB_E_BADCOMPAREOP. Esto es coherente con la especificación OLE DB.  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
