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
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 35aeb96485085910467c0fbca663c4161ffdff40
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720601"
---
# <a name="validate-subscriptions"></a>Validar suscripciones
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/applies-to-version/sql-asdb.md)]
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
  
  
