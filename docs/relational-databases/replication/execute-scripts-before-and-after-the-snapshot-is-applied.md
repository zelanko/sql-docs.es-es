---
title: "Ejecutar scripts antes y después de aplicar la instantánea | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
- scripts [SQL Server replication]
ms.assetid: 9a6872c2-9bed-477f-9d2f-332d640edcf2
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01d55924d79b7291b23aab38ae06e0a2112c0978
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="execute-scripts-before-and-after-the-snapshot-is-applied"></a>Ejecutar scripts antes y después de aplicar la instantánea
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Puede especificar scripts que se ejecuten en el suscriptor antes o después de aplicar la instantánea. Los scripts pueden utilizarse por distintos motivos, por ejemplo, para crear inicios de sesión y esquemas (propietarios de objetos) en cada suscriptor.  
  
 Al especificar una ubicación de archivos para cada script, el Agente de instantáneas copia los archivos de script en la carpeta actual de instantáneas cada vez que se procesan instantáneas. El Agente de distribución o el Agente de mezcla ejecutan el script previo a la instantánea antes que cualquiera de los scripts de objetos replicados al aplicar una instantánea. El Agente de distribución o el Agente de mezcla ejecutan el script posterior a la instantánea después de aplicar todos los demás datos y scripts de objetos replicados. Después de completar la aplicación de instantáneas y de ejecutar correctamente los archivos de script, estos archivos se quitan del directorio de trabajo del suscriptor.  
  
 El script se ejecuta con la utilidad **sqlcmd** . Antes de implementar un script, ejecútelo con **sqlcmd** para asegurarse de que se ejecuta según lo previsto. El contenido de los scripts que se ejecutan antes y después de aplicar la instantánea debe ser repetible. Por ejemplo, si crea una tabla en el script, debe comprobar primero si ya existe y tomar las medidas apropiadas si no existe. El script debe ser repetible, porque si necesita reinicializar una suscripción en la que ya se aplicó el script, este se volverá a aplicar cuando se aplique la nueva instantánea durante la reinicialización.  
  
 Si comprime el archivo de instantáneas en formato CAB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , los scripts también se comprimen y se colocan en el archivo CAB. Después de que el archivo de instantáneas comprimido se transfiere al suscriptor y se descomprime en un directorio de trabajo del suscriptor, se ejecutan los scripts indicados como anteriores a la instantánea. De la misma manera, los scripts posteriores a la instantánea se descomprimen y se ejecutan en el suscriptor como el último paso para la aplicación de la instantánea.  
  
 **Para ejecutar los scripts antes y después de aplicar la instantánea**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Cómo ejecutar scripts antes y después de aplicar una instantánea \(SQL Server Management Studio\)](../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   Programación de la replicación con [!INCLUDE[tsql](../../includes/tsql-md.md)]: [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Ver también  
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Opciones de instantánea](../../relational-databases/replication/snapshot-options.md)  
  
  
