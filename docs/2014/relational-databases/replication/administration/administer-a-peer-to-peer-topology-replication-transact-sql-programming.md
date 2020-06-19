---
title: Administrar una topología punto a punto (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3a73af1c1f3a7196d87f77681ee9d62a3ef248a4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068778"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>Administrar una topología punto a punto (programación de la replicación con Transact-SQL)
  Administrar una topología punto a punto es parecido a administrar una topología de replicación transaccional típica, pero hay varios aspectos que requieren una consideración especial. La diferencia principal cuando se administra una topología punto a punto es que algunos cambios requieren que el sistema esté *detenido*. Para poner el sistema en modo inactivo, hay que detener la actividad de las tablas publicadas en todos los nodos y asegurarse de que cada nodo haya recibido todos los cambios de los demás nodos. Para más información, vea [Poner en modo inactivo una topología de replicación &#40;programación de la replicación con Transact-SQL&#41;](quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
> [!NOTE]  
>  En una topología punto a punto, el distribuidor no puede utilizar una versión anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que la de un suscriptor de extracción.  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>Agregar un artículo a una configuración existente  
  
1.  Detenga el sistema.  
  
2.  Detenga el Agente de distribución en cada nodo de la topología. Para más información, vea [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md) o [Iniciar y detener un Agente de replicación &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Ejecute la instrucción CREATE TABLE para agregar la nueva tabla en cada nodo de la topología.  
  
4.  Realice una copia masiva de los datos de la nueva tabla manualmente en todos los nodos mediante la utilidad [bcp](../../../tools/bcp-utility.md).  
  
5.  Ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) para crear el nuevo artículo en cada nodo en la topología. Para más información, consulte [Define an Article](../publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Una vez ejecutado [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) , la replicación agrega automáticamente el artículo a las suscripciones de la topología.  
  
6.  Reinicie los agentes de distribución en cada nodo de la topología.  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>Para realizar cambios del esquema en una base de datos de publicación  
  
1.  Detenga el sistema.  
  
2.  Ejecute las instrucciones de lenguaje de definición de datos (DDL) para modificar el esquema de tablas publicadas. Para más información sobre los cambios de esquema admitidos, vea [Realizar cambios de esquema en bases de datos de publicaciones](../publish/make-schema-changes-on-publication-databases.md).  
  
3.  Antes de reanudar la actividad en tablas publicadas, detenga el sistema de nuevo. De esta manera se garantiza que los cambios del esquema se han recibido en todos los nodos antes de que se haya replicado cualquier nuevo cambio de los datos.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo agregar un nuevo artículo de tabla a una topología de replicación punto a punto existente con dos nodos.  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createtables)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_cmdline)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createarticle)]  
  
## <a name="see-also"></a>Consulte también  
 [Preguntas más frecuentes sobre la administración de replicación](frequently-asked-questions-for-replication-administrators.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Peer-to-Peer Transactional Replication](../transactional/peer-to-peer-transactional-replication.md)  
  
  
