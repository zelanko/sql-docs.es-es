---
title: Ejecutar scripts durante la sincronización (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 6d408f214d9cc08ec75450c6e9e2ef3abd0f8fc3
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39554495"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Ejecutar scripts durante la sincronización (programación de la replicación con Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La replicación admite la ejecución de script a petición para suscriptores a publicaciones transaccionales y de combinación. Esta funcionalidad copia el script en el directorio de trabajo de la replicación y, a continuación, usa **sqlcmd** para aplicar el script en el suscriptor. De forma predeterminada, si hay un error al aplicar el script para una suscripción a una publicación transaccional, el Agente de distribución se detendrá. Puede especificar que un script [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecute mediante programación con los procedimientos almacenados de la replicación.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>Para especificar que un script se ejecute para todos los suscriptores a una publicación transaccional, de instantáneas o de combinación  
  
1.  Cree y pruebe el script [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecutará a petición.  
  
2.  Guarde el archivo de script en una ubicación en la que pueda tener acceso el Agente de instantáneas de la publicación.  
  
3.  En el publicador de la base de datos de publicaciones, ejecute [sp_addscriptexec &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Especifique **@publication**, el nombre del archivo de script con la ruta UNC completa creada en el paso 2 para **@scriptfile**y uno de los valores siguientes para **@skiperror**:  
  
    -   **0** - el agente dejará de ejecutar el script si se encuentra un error.  
  
    -   **1** - el agente registrará los errores y continuará ejecutando el script cuando se encuentren errores.  
  
4.  El script especificado se ejecutará en cada suscriptor cuando el agente se vuelva a ejecutar para sincronizar la suscripción.  
  
## <a name="see-also"></a>Ver también  
 [Sincronizar datos](../../relational-databases/replication/synchronize-data.md)  
  
  
