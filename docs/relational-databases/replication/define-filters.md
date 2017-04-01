---
title: "Definir filtros | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replconflictviewer.definefilters.f1"
helpviewer_keywords: 
  - "Definir filtros, cuadro de diálogo"
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Definir filtros
  El cuadro de diálogo **Definir filtros** permite definir filtros que posteriormente se aplican a conflictos de datos para obtener un subconjunto de conflictos en la cuadrícula. Para definir un filtro, seleccione un operador desde el **operador** lista desplegable cuadro y, a continuación, escriba un valor. Por ejemplo, para mostrar solamente los conflictos en los que el perdedor del conflicto es server **ReplTest1**, seleccione **igual a** desde el **operador** lista desplegable cuadro y escriba **ReplTest1** en la primera **valor** columna.  
  
## Opciones  
 **Operador**  
 Seleccione un operador para el filtro, como **menor o igual a**.  
  
 **Valor**  
 Escriba un valor para el filtro. La mayoría de los operadores solo requiere un valor en la primera columna **Valor** ; sin embargo, los operadores **Entre** y **No entre** requieren un valor en las dos columnas **Valor** .  
  
 **Desactivar**  
 Haga clic en este botón para borrar todos los filtros previamente definidos.  
  
## Vea también  
 [Visor de conflictos de replicación de Microsoft & #40; La replicación de mezcla & #41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Visor de conflictos de replicación de Microsoft & #40; La replicación transaccional & #41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  