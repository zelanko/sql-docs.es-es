---
title: Realizar una actualización ficticia de un artículo de mezcla (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_mergedummyupdate
- dummy updates [SQL Server replication]
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 07fa0f868b2c3f98496046b138424d7d3a2fa2fd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010999"
---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>Realizar una actualización ficticia de un artículo de mezcla (programación de la replicación con Transact-SQL)
  La replicación de mezcla utiliza los desencadenadores como parte del proceso de la replicación; cuando se actualiza una tabla tabla publicada, se activa un desencadenador de actualización. En algunos casos, los datos pueden actualizarse sin que el desencadenador se active, como durante las operaciones de UPDATETEXT y WRITETEXT. En estos casos, necesita agregar explícitamente una instrucción UPDATE ficticia para replicar el cambio. Puede agregar una instrucción UPDATE ficticia mediante los procedimientos almacenados de replicación.  
  
### <a name="to-add-a-dummy-update-statement"></a>Para agregar una instrucción UPDATE ficticia  
  
1.  Ejecute la operación (por ejemplo, UPDATETEXT) en una fila de una tabla publicada de mezcla que requiera una actualización ficticia.  
  
2.  En el servidor (publicador o suscriptor) de la base de datos donde se realizó la modificación, ejecute [sp_mergedummyupdate &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql). Especifique la tabla en la que se realizó el cambio **@source_object** y el identificador único de la fila modificada para **@rowguid** .  
  
3.  Sincronice la suscripción para replicar la fila cambiada.  
  
  
