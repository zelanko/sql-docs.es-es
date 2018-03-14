---
title: Acciones comunes que requieren una copia de seguridad actualizada | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- recovery [SQL Server replication], actions requiring a backup
- restoring [SQL Server replication], actions requiring a backup
- backups [SQL Server replication], actions requiring a backup
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4cc5303d5253c1621b5b5f62105f5a3e5e26d23
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="common-actions-requiring-an-updated-backup"></a>Acciones comunes que requieren una copia de seguridad actualizada
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si realiza regularmente copias de seguridad de registros, éstas deben capturar todos los cambios relacionados con la replicación. Si no realiza copias de seguridad de registros, cree una copia de seguridad de las bases de datos de publicaciones, distribución, suscripciones, **msdb**y **maestra** después de realizar modificaciones en la topología o en el esquema de replicación.  
  
## <a name="publication-database"></a>Base de datos de publicaciones  
 Haga una copia de seguridad de la base de datos de publicaciones después de:  
  
-   Crear nuevas publicaciones.  
  
-   Modificar una propiedad de publicación, incluido el filtro.  
  
-   Agregar artículos a una publicación ya existente.  
  
-   Reinicializar las suscripciones de todas las publicaciones.  
  
-   Realizar cambios de esquema en una tabla publicada.  
  
-   Realizar la ejecución de script a petición con [sp_addscriptexec &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md).  
  
-   Cambiar cualquier propiedad de un artículo.  
  
-   Quitar publicaciones.  
  
-   Quitar artículos.  
  
-   Deshabilitar la replicación.  
  
## <a name="distribution-database"></a>Base de datos de distribución  
 Haga una copia de seguridad de la base de datos de distribución después de:  
  
-   Crear o modificar perfiles de agente de replicación.  
  
-   Modificar parámetros de un perfil de agente de replicación.  
  
-   Cambiar las propiedades del agente de replicación (incluidas las programaciones) para las suscripciones de inserción.  
  
-   La función de administración automática de intervalos de identidades asigna un nuevo intervalo de identidades.  
  
## <a name="subscription-database"></a>Base de datos de suscripciones  
 Haga una copia de seguridad de la base de datos de suscripciones después de:  
  
-   Cambiar una propiedad de suscripción.  
  
-   Cambiar la prioridad de una suscripción de mezcla en el publicador.  
  
-   Quitar suscripciones.  
  
-   Deshabilitar la replicación.  
  
## <a name="msdb-database"></a>Base de datos msdb  
 Cree una copia de seguridad de la base de datos **msdb** del sistema en el nodo apropiado después de:  
  
-   Habilitar o deshabilitar la replicación.  
  
-   Agregar o quitar una base de datos de distribución (en el distribuidor).  
  
-   Habilitar o deshabilitar la publicación de una base de datos (en el publicador).  
  
-   Crear o modificar perfiles de agente de replicación (en el distribuidor).  
  
-   Modificar parámetros del perfil de agente de replicación (en el distribuidor).  
  
-   Cambiar las propiedades del agente de replicación (incluidas las programaciones) para las suscripciones de inserción (en el distribuidor).  
  
-   Cambiar las propiedades del agente de replicación (incluidas las programaciones) para las suscripciones de extracción (en el suscriptor).  
  
-   Crear un paquete DTS asociado con una publicación transaccional que utilice suscripciones transformables (en el distribuidor y en el suscriptor).  
  
-   Agregar o quitar una suscripción transformable (en el distribuidor y en el suscriptor).  
  
## <a name="master-database"></a>Base de datos maestra  
 Cree una copia de seguridad de la base de datos del sistema **mestra** en el nodo apropiado después de:  
  
-   Habilitar o deshabilitar la replicación.  
  
-   Agregar o quitar una base de datos de distribución (en el distribuidor).  
  
-   Habilitar o deshabilitar la publicación de una base de datos (en el publicador).  
  
-   Agregar la primera o quitar la última publicación en una base de datos (en el publicador).  
  
-   Agregar la primera o quitar la última suscripción en una base de datos (en el suscriptor).  
  
-   Habilitar o deshabilitar un publicador en un publicador de distribución (en el publicador y el distribuidor).  
  
## <a name="see-also"></a>Ver también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  
