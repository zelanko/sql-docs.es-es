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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fba42b0cd532f61dc71c89ba67c09798f69891fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836683"
---
# <a name="validate-subscriptions"></a>Validar suscripciones
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Utilice el cuadro de diálogo **Validar suscripciones** para especificar que las suscripciones a una publicación transaccional se deben validar la próxima vez que se ejecute el Agente de distribución para cada suscripción. El resultado de la validación se muestra en el Monitor de replicación. Para más información, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
## <a name="options"></a>Opciones  
 **Validar todas las suscripciones de SQL Server**  
 Seleccione esta opción para validar datos de todas las suscripciones de SQL Server para esta publicación.  
  
 **Validar las siguientes suscripciones**  
 Seleccione esta opción si no desea validar todas las suscripciones. Para ello, seleccione de la lista las suscripciones que desea validar.  
  
 **Opciones de validación**  
 Haga clic para tener acceso al cuadro de diálogo **Opciones de validación de subscripciones** , que permite especificar si desea usar la validación del recuento de filas o la validación de las sumas de comprobación binarias.  
  
## <a name="see-also"></a>Ver también  
 [Validar datos replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  
