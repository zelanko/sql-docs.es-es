---
title: "Replicación de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
caps.latest.revision: "58"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: a938161a6f9d748e4329485c56257bda097bbadc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-replication"></a>Replicación de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La replicación es un conjunto de tecnologías destinadas a la copia y distribución de datos y objetos de base de datos de una base de datos a otra, para luego sincronizar ambas bases de datos con el fin de mantener su coherencia. Utilice la replicación para distribuir datos entre diferentes ubicaciones y entre usuarios remotos o móviles mediante redes locales y de área extensa, conexiones de acceso telefónico, conexiones inalámbricas e Internet.  
  
 La replicación transaccional se usa normalmente en escenarios servidor a servidor que requieren un alto rendimiento, como por ejemplo, la mejora de la escalabilidad y la disponibilidad, el almacenamiento de datos y la creación de informes, la integración de datos procedentes de varios sitios, la integración de datos heterogéneos, y la descarga del procesamiento por lotes. La replicación de mezcla se ha diseñado principalmente para las aplicaciones móviles o de servidores distribuidos que pueden encontrarse con conflictos de datos. Los escenarios más frecuentes son: el intercambio de datos con usuarios móviles, las aplicaciones de punto de venta (POS) a consumidores, y la integración de datos de varios sitios. La replicación de instantáneas se usa para proporcionar el conjunto de datos inicial para la replicación transaccional y de mezcla; también se puede usar cuando está indicada una actualización completa de los datos. Con estos tres tipos de replicación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un sistema eficaz y flexible para la sincronización de datos en toda la organización. La replicación en SQLCE 3.5 y SQLCE 4.0 se admite tanto en [!INCLUDE[win8srv](../../includes/win8srv-md.md)] como en [!INCLUDE[win8](../../includes/win8-md.md)].  
  
 Como alternativa a la replicación, puede sincronizar bases de datos mediante Microsoft Sync Framework. Sync Framework incluye componentes y una API intuitiva y flexible que facilitan la sincronización entre bases de datos de SQL Server, SQL Server Express, SQL Server Compact y SQL Azure. Sync Framework también incluye clases que se pueden adaptar para sincronizar entre una base de datos de SQL Server y cualquier otra base de datos compatible con ADO.NET. Para obtener documentación detallada de los componentes de sincronización de base de datos de Sync Framework, vea [Sincronizar bases de datos](http://go.microsoft.com/fwlink/?LinkId=209079). Para obtener información general sobre Sync Framework, vea el [Centro para desarrolladores de Microsoft Sync Framework](http://go.microsoft.com/fwlink/?LinkId=209078). Para obtener una comparación entre Sync Framework y la replicación de mezcla, vea [Información general y escenarios](http://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  
 **Examinar por área**  
 - [Novedades](../../relational-databases/replication/what-s-new-replication.md)  
 - [Compatibilidad con versiones anteriores](../../relational-databases/replication/replication-backward-compatibility.md)  
 - [Características y tareas de replicación](../../relational-databases/replication/replication-features-and-tasks.md)  
 - [Referencia técnica](../../relational-databases/replication/technical-reference-replication.md)  
  
  
