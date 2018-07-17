---
title: Administración de inicios de sesión en la lista de acceso a la publicación | Microsoft Docs
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
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- logins [SQL Server replication], managing
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
caps.latest.revision: 45
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 76ae4087878b5a25b28714f70322778ecb1af344
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37360129"
---
# <a name="manage-logins-in-the-publication-access-list"></a>Administrar inicios de sesión en la lista de acceso a la publicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo administrar inicios de sesión en la lista de acceso a la publicación (PAL) en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La lista de acceso a la publicación (PAL) controla el acceso a una publicación. Se pueden agregar y quitar inicios de sesión y grupos de la PAL.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
-   **Para administrar inicios de sesión en la lista de acceso a la publicación con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe asociar el inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un usuario de la base de datos de publicaciones antes de agregar el inicio de sesión a la PAL.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Use la lista de acceso a la publicación (PAL) de la página **Lista de acceso a la publicación** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** para administrar los inicios de sesión. Para obtener más información sobre cómo acceder a este cuadro de diálogo, vea [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-manage-logins-in-the-pal"></a>Para administrar inicios de sesión en la lista de acceso de la publicación  
  
1.  En la página **Lista de acceso a la publicación** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**, use los botones **Agregar**, **Quitar** y **Quitar todo** para agregar y quitar inicios de sesión y grupos de la PAL. No quite **distributor_admin** de la PAL. La replicación utiliza esta cuenta.  
  
    > [!NOTE]  
    >  Si se utiliza un distribuidor remoto, las cuentas de la lista de acceso de la publicación deben estar disponibles tanto en el publicador como en el distribuidor. La cuenta debe ser una cuenta de dominio o una cuenta local que esté definida en ambos servidores. Las contraseñas asociadas a ambos inicios de sesión deben ser iguales.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-groups-and-logins-that-belong-to-the-pal"></a>Para ver los grupos y los inicios de sesión que pertenecen a la PAL  
  
1.  En el publicador de la base de datos de publicaciones, ejecute [sp_help_publication_access](../../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md). Para **@publication**, especifique el nombre de la publicación. Esto muestra información acerca de los grupos y los inicios de sesión en la PAL.  
  
#### <a name="to-add-groups-and-logins-to-the-pal"></a>Para agregar grupos e inicios de sesión a la PAL  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_grant_publication_access](../../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md). Para **@publication**, especifique el nombre de la publicación; y para **@login**, especifique el nombre del inicio de sesión o del grupo que se agrega.  
  
#### <a name="to-remove-groups-and-logins-from-the-pal"></a>Para quitar grupos e inicios de sesión de la PAL  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_revoke_publication_access](../../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md). Para **@publication**, especifique el nombre de la publicación; y para **@login**, especifique el nombre del inicio de sesión o del grupo que se quita.  
  
## <a name="see-also"></a>Ver también  
 [Administrar inicios de sesión en la lista de acceso a la publicación](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)   
 [Modelo de seguridad del Agente de replicación](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Proteger una topología de replicación](../../../relational-databases/replication/security/secure-a-replication-topology.md)   
 [Proteger al publicador](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  
