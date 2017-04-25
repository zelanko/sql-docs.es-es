---
title: "Suscripción, Comandos sin distribuir (Suscripción transaccional) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3986838ebcbb9f5ed787c974b82e9a87f2a43a29
ms.lasthandoff: 04/11/2017

---
# <a name="subscription-undistributed-commands-transactional-subscription"></a>Suscripción, Comandos sin distribuir (Suscripción transaccional)
  En la pestaña **Comandos sin distribuir** se muestra información sobre le número de comandos de la base de datos de distribución que no se han entregado al suscriptor seleccionado y el tiempo estimado para entregar esos comandos. Para información sobre cómo ver los comandos en la base de datos de distribución, vea [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md).  
  
## <a name="options"></a>Opciones  
 **Número de comandos en la base de datos de distribución en espera de ser aplicados al suscriptor**  
 Número de comandos de la base de datos de distribución que no se han entregado al suscriptor seleccionado. Un comando se compone de una instrucción de lenguaje de manipulación de datos (DML) de Transact-SQL o una instrucción de lenguaje de definición de datos (DDL).  
  
 **Tiempo estimado para aplicar estos comandos según las últimas operaciones**  
 Cantidad estimada de tiempo para entregar comandos al suscriptor. Si este valor es superior al tiempo necesario para generar y aplicar una instantánea en el suscriptor, considere la posibilidad de volver a reinicializar el suscriptor. Para obtener más información, vea [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Supervisar el rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
