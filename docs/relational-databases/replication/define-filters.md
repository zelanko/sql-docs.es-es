---
title: Definición de filtros | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ef180ac401b540d1abe50688b98e691c819f55f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85654059"
---
# <a name="define-filters"></a>Definir filtros
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El cuadro de diálogo **Definir filtros** permite definir filtros que posteriormente se aplican a conflictos de datos para obtener un subconjunto de conflictos en la cuadrícula. Para definir un filtro, elija un operador del cuadro de lista desplegable **Operador** y, a continuación, especifique un valor. Por ejemplo, si desea mostrar solamente los conflictos en los que el perdedor del conflicto es el servidor **ReplTest1**, seleccione **Igual a** en el cuadro de lista desplegable **Operador** y especifique **ReplTest1** en la primera columna **Valor** .  
  
## <a name="options"></a>Opciones  
 **Operador**  
 Seleccione un operador para el filtro, como por ejemplo **Menor o igual que**.
  
 **Valor**  
 Escriba un valor para el filtro. La mayoría de los operadores solo requiere un valor en la primera columna **Valor** ; sin embargo, los operadores **Entre** y **No entre** requieren un valor en las dos columnas **Valor** .  
  
 **Borrar**  
 Haga clic en este botón para borrar todos los filtros previamente definidos.  
  
## <a name="see-also"></a>Consulte también  
 [Visor de conflictos de replicación de Microsoft &#40;Replicación de mezcla&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Visor de conflictos de replicación de Microsoft &#40;Replicación transaccional&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
