---
title: Inicializar una suscripción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1f024d360fdeab477ace09970b4f140a97696c2c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068678"
---
# <a name="initialize-a-subscription"></a>Inicializar una suscripción
  Los suscriptores de una topología de replicación se deben inicializar con el fin de que tengan una copia del esquema de cada artículo de la publicación a la que están suscritos y de los objetos de replicación que se requieran, como procedimientos almacenados, desencadenadores y tablas de metadatos. Además, el suscriptor normalmente recibe un conjunto de datos inicial. El método de inicialización predeterminado usa una instantánea completa que incluye el esquema, objetos de replicación y datos, aunque las publicaciones también se pueden inicializar sin una instantánea completa.  
  
 Para obtener más información, consulte [Initialize a Subscription with a Snapshot](initialize-a-subscription-with-a-snapshot.md) y [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
