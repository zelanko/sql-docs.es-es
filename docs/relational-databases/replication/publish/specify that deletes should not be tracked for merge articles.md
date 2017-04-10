---
title: "Especificar que no se debe realizar un seguimiento de las eliminaciones para los art&#237;culos de mezcla (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "seguimiento condicional de eliminaciones [replicación de SQL Server]"
  - "replicación de mezcla [replicación de SQL Server], seguimiento de eliminación condicional"
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Especificar que no se debe realizar un seguimiento de las eliminaciones para los art&#237;culos de mezcla (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 De forma predeterminada, la replicación de mezcla sincroniza los comandos DELETE entre el Publicador y Suscriptor. La replicación de mezcla le permite conservar filas en la base de datos de suscripciones incluso cuando se han eliminado de la publicación, y viceversa. Puede especificar mediante programación que se omitan los comandos DELETE al crear un nuevo artículo o puede habilitar esta funcionalidad en un momento posterior usando los procedimientos almacenados de replicación.  
  
> [!IMPORTANT]  
>  Al habilitar esta funcionalidad se producirá la no convergencia, lo que significa que los datos presentes en el Suscriptor no reflejarán con precisión los datos en el Publicador. Debe implementar su propio mecanismo para quitar manualmente las filas eliminadas.  
  
### Para especificar que se omitan las eliminaciones para un nuevo artículo de mezcla  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique un valor de **false** para **@delete_tracking**. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Si la tabla de origen para un artículo ya está publicada en otra publicación, el valor de **delete_tracking** debe ser el mismo para ambos artículos.  
  
### Para especificar que se omitan las eliminaciones para un artículo de mezcla existente  
  
1.  Para determinar si está habilitada la compensación de errores para un artículo, ejecute [sp_helpmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) Tenga en cuenta el valor de **delete_tracking** conjunto de resultados. Si este valor es **0**, ya se están omitiendo las eliminaciones.  
  
2.  Si el valor del paso 1 es **1**, ejecute [sp_changemergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **delete_tracking** para **@property**, y un valor de **false** para **@value**.  
  
    > [!NOTE]  
    >  Si la tabla de origen para un artículo ya está publicada en otra publicación, el valor de **delete_tracking** debe ser el mismo para ambos artículos.  
  
## Vea también  
 [Optimizar el rendimiento de la replicación de mezcla con seguimiento condicional de eliminaciones](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  