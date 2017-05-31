---
title: Acciones comunes que requieren una copia de seguridad actualizada | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- recovery [SQL Server replication], actions requiring a backup
- restoring [SQL Server replication], actions requiring a backup
- backups [SQL Server replication], actions requiring a backup
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8784d006b175b3b6471464f401ad460080a273a
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="common-actions-requiring-an-updated-backup"></a>Acciones comunes que requieren una copia de seguridad actualizada
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
  
## <a name="see-also"></a>Vea también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  
