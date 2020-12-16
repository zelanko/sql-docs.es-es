---
title: Comandos sin distribuir (Monitor de replicación)
description: Describe la pestaña "Comandos sin distribuir" del Monitor de replicación en SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: eec70665ef299b54c07ee74a4189ff3a10d00482
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460168"
---
# <a name="subscription-undistributed-commands-transactional-subscription"></a>Suscripción, Comandos sin distribuir (Suscripción transaccional)
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  En la pestaña **Comandos sin distribuir** se muestra información sobre le número de comandos de la base de datos de distribución que no se han entregado al suscriptor seleccionado y el tiempo estimado para entregar esos comandos. Para información sobre cómo ver los comandos en la base de datos de distribución, vea [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md).  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opciones  
 **Número de comandos en la base de datos de distribución en espera de ser aplicados al suscriptor**  
 Número de comandos de la base de datos de distribución que no se han entregado al suscriptor seleccionado. Un comando se compone de una instrucción de lenguaje de manipulación de datos (DML) de Transact-SQL o una instrucción de lenguaje de definición de datos (DDL).  
  
 **Tiempo estimado para aplicar estos comandos según las últimas operaciones**  
 Cantidad estimada de tiempo para entregar comandos al suscriptor. Si este valor es superior al tiempo necesario para generar y aplicar una instantánea en el suscriptor, considere la posibilidad de volver a reinicializar el suscriptor. Para obtener más información, vea [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Supervisar el rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
