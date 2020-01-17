---
title: Ejecución de scripts durante la sincronización (procedimientos almacenados de replicación)
description: Obtenga información sobre cómo usar los procedimientos almacenados de replicación para ejecutar scripts a petición durante el proceso de sincronización de una publicación transaccional o de combinación.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d1027e969c12f5b5234f05bfeef12c7b93e3de84
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321733"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Ejecutar scripts durante la sincronización (programación de la replicación con Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replicación admite la ejecución de script a petición para suscriptores a publicaciones transaccionales y de combinación. Esta funcionalidad copia el script en el directorio de trabajo de la replicación y, a continuación, usa **sqlcmd** para aplicar el script en el suscriptor. De forma predeterminada, si hay un error al aplicar el script para una suscripción a una publicación transaccional, el Agente de distribución se detendrá. Puede especificar que un script [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecute mediante programación con los procedimientos almacenados de la replicación.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>Para especificar que un script se ejecute para todos los suscriptores a una publicación transaccional, de instantáneas o de combinación  
  
1.  Cree y pruebe el script [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecutará a petición.  
  
2.  Guarde el archivo de script en una ubicación en la que pueda tener acceso el Agente de instantáneas de la publicación.  
  
3.  En el publicador de la base de datos de publicaciones, ejecute [sp_addscriptexec &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Especifique `@publication`, el nombre del archivo de script con la ruta de acceso UNC completa creada en el paso 2 para `@scriptfile` y uno de los valores siguientes para `@skiperror`:  
  
    -   **0** - el agente dejará de ejecutar el script si se encuentra un error.  
  
    -   **1** - el agente registrará los errores y continuará ejecutando el script cuando se encuentren errores.  
  
4.  El script especificado se ejecutará en cada suscriptor cuando el agente se vuelva a ejecutar para sincronizar la suscripción.  
  
## <a name="see-also"></a>Consulte también  
 [Sincronizar datos](../../relational-databases/replication/synchronize-data.md)  
  
  
