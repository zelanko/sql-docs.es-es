---
title: Administrar una topología punto a punto (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 47a04d8e37b57d3a7496aaf55909a91de4881a92
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356597"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>Administrar una topología punto a punto (programación de la replicación con Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Administrar una topología punto a punto es parecido a administrar una topología de replicación transaccional típica, pero hay varios aspectos que requieren una consideración especial. La diferencia principal cuando se administra una topología punto a punto es que algunos cambios requieren que el sistema esté *detenido*. Para poner el sistema en modo inactivo, hay que detener la actividad de las tablas publicadas en todos los nodos y asegurarse de que cada nodo haya recibido todos los cambios de los demás nodos. Para más información, vea [Poner en modo inactivo una topología de replicación &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
> [!NOTE]  
>  En una topología punto a punto, el distribuidor no puede utilizar una versión anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que la de un suscriptor de extracción.  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>Agregar un artículo a una configuración existente  
  
1.  Detenga el sistema.  
  
2.  Detenga el Agente de distribución en cada nodo de la topología. Para más información, vea [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [Iniciar y detener un Agente de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Ejecute la instrucción CREATE TABLE para agregar la nueva tabla en cada nodo de la topología.  
  
4.  Realice una copia masiva de los datos de la nueva tabla manualmente en todos los nodos mediante la utilidad [bcp](../../../tools/bcp-utility.md).  
  
5.  Ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) para crear el nuevo artículo en cada nodo de la topología. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Una vez ejecutado [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), la replicación agrega automáticamente el artículo a las suscripciones de la topología.  
  
6.  Reinicie los agentes de distribución en cada nodo de la topología.  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>Para realizar cambios del esquema en una base de datos de publicación  
  
1.  Detenga el sistema.  
  
2.  Ejecute las instrucciones de lenguaje de definición de datos (DDL) para modificar el esquema de tablas publicadas. Para más información sobre los cambios de esquema admitidos, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
3.  Antes de reanudar la actividad en tablas publicadas, detenga el sistema de nuevo. De esta manera se garantiza que los cambios del esquema se han recibido en todos los nodos antes de que se haya replicado cualquier nuevo cambio de los datos.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo agregar un nuevo artículo de tabla a una topología de replicación punto a punto existente con dos nodos.  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_1.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_2.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_3.sql)]  
  
## <a name="see-also"></a>Ver también  
 [Administración &#40;replicación&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Replicación transaccional punto a punto](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
