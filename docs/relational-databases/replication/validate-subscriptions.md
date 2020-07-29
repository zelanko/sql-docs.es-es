---
title: Validar suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.subscriptions.f1
helpviewer_keywords:
- Validate Subscriptions dialog box
ms.assetid: 0ca39a35-f22c-46c5-82a4-342e34bf5d1b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 79079774fe3b13e61a9bbdb32c767c2f40576b66
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "87110519"
---
# <a name="validate-subscriptions"></a>Validar suscripciones
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  Utilice el cuadro de diálogo **Validar suscripciones** para especificar que las suscripciones a una publicación transaccional se deben validar la próxima vez que se ejecute el Agente de distribución para cada suscripción. El resultado de la validación se muestra en el Monitor de replicación. Para más información, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opciones  
 **Validar todas las suscripciones de SQL Server**  
 Seleccione esta opción para validar datos de todas las suscripciones de SQL Server para esta publicación.  
  
 **Validar las siguientes suscripciones**  
 Seleccione esta opción si no desea validar todas las suscripciones. Para ello, seleccione de la lista las suscripciones que desea validar.  
  
 **Opciones de validación**  
 Haga clic para tener acceso al cuadro de diálogo **Opciones de validación de subscripciones** , que permite especificar si desea usar la validación del recuento de filas o la validación de las sumas de comprobación binarias.  
  
## <a name="see-also"></a>Consulte también  
 [Validar datos replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
