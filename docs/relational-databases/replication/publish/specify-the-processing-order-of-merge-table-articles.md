---
title: Especificar el orden de procesamiento de los artículos de tabla de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1bec5a8d14adf65bbf8df5d149e79b5299327c0c
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37348817"
---
# <a name="specify-the-processing-order-of-merge-table-articles"></a>Especificar el orden de procesamiento de los artículos de tabla de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replicación de mezcla le permite especificar el orden en el que el Agente de mezcla procesa los artículos durante el proceso de sincronización. Al crear cada artículo, puede asignarle un orden mediante programación utilizando los procedimientos almacenados de replicación. Los artículos se procesan en orden desde el valor menor al mayor. Si existen dos artículos que tienen el mismo valor, se procesan al mismo tiempo. Para obtener más información, vea [Especificar el orden de procesamiento de los artículos de mezcla](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
### <a name="to-specify-the-processing-order-for-a-new-merge-article"></a>Para especificar el orden de procesamiento de un nuevo artículo de mezcla  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique un valor entero que represente el orden de procesamiento del artículo en **@processing_order**. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Al crear artículos ordenados, debería dejar huecos entre los valores de orden de los artículos. Esto le permitirá establecer nuevos valores en el futuro con mayor facilidad. Por ejemplo, si tiene tres artículos para los que necesita especificar un orden de procesamiento fijo, establezca el valor **@processing_order** en 10, 20 y 30 en lugar de 1, 2 y 3, respectivamente.  
  
### <a name="to-change-the-processing-order-of-a-merge-article"></a>Para cambiar el orden de procesamiento de un artículo de mezcla  
  
1.  Para determinar orden de procesamiento de un artículo, ejecute [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) y tenga en cuenta el valor de **processing_order** en el conjunto de resultados.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique el valor **processing_order** para **@property** y un valor entero que represente el orden de procesamiento para **@value**.  
  
## <a name="see-also"></a>Ver también  
 [Especificar el orden de procesamiento de los artículos de mezcla](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)  
  
  
