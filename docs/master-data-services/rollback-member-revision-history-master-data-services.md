---
title: "Reversión del historial de revisiones de miembro (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
caps.latest.revision: 5
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a242f91eb8259b8941a61db94f59c4e331d5b06b
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="rollback-member-revision-history-master-data-services"></a>Reversión del historial de revisiones de miembro (Master Data Services)
  Cada vez que se cambia un miembro, se registra un historial de revisiones de miembro. Se puede revertir un historial de revisiones de miembro a una versión anterior.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe tener permiso para actualizar al menos uno de los atributos del miembro seleccionado. Al revertir un historial de revisiones, todos los valores de atributo que se puedan actualizar se revertirán a los valores de la versión anterior.  
  
-   El historial de revisiones solo está disponible cuando el tipo de registro de transacciones de la entidad es miembro.  
  
 **Para revertir el historial de revisiones de miembro**  
  
1.  En Master Data Manager, haga clic en Explorador.  
  
2.  Elija la entidad y el miembro de la reversión.  
  
3.  Haga clic en **Ver historial**.  
  
4.  Elija la revisión para revertir y luego haga clic en **Revertir**.  
  
## <a name="see-also"></a>Vea también  
 [Historial de revisiones de miembro &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [Cambio del tipo de registro de transacciones de entidad &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  

