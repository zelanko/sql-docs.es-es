---
title: Administración de inicios de sesión en la lista de acceso a la publicación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- logins [SQL Server replication], managing
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b96e6f46403cf3a482f00a3f5155527177920967
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85009913"
---
# <a name="manage-logins-in-the-publication-access-list"></a>Administrar inicios de sesión en la lista de acceso a la publicación
  En este tema se describe cómo administrar inicios de sesión en la lista de acceso a la publicación (PAL) en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La lista de acceso a la publicación (PAL) controla el acceso a una publicación. Se pueden agregar y quitar inicios de sesión y grupos de la PAL.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
-   **Para administrar inicios de sesión en la lista de acceso a la publicación con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
  
-   Debe asociar el inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un usuario de la base de datos de publicaciones antes de agregar el inicio de sesión a la PAL.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Utilice la lista de acceso a la publicación (PAL) de la página **lista de acceso a** la publicación del cuadro de diálogo Propiedades de la **publicación \<Publication> :** para administrar los inicios de sesión. Para obtener más información sobre cómo acceder a este cuadro de diálogo, vea [Ver y modificar propiedades de publicación](../publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-manage-logins-in-the-pal"></a>Para administrar inicios de sesión en la lista de acceso de la publicación  
  
1.  En la página **lista de acceso a la publicación** del cuadro de diálogo Propiedades de la **publicación: \<Publication> ** , use los botones **Agregar**, **quitar**y **quitar todo** para agregar y quitar inicios de sesión y grupos de la PAL. No quite **distributor_admin** de la PAL. La replicación utiliza esta cuenta.  
  
    > [!NOTE]  
    >  Si se utiliza un distribuidor remoto, las cuentas de la lista de acceso de la publicación deben estar disponibles tanto en el publicador como en el distribuidor. La cuenta debe ser una cuenta de dominio o una cuenta local que esté definida en ambos servidores. Las contraseñas asociadas a ambos inicios de sesión deben ser iguales.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-groups-and-logins-that-belong-to-the-pal"></a>Para ver los grupos y los inicios de sesión que pertenecen a la PAL  
  
1.  En el publicador de la base de datos de publicaciones, ejecute [sp_help_publication_access](/sql/relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql). En ** \@ publicación**, especifique el nombre de la publicación. Esto muestra información acerca de los grupos y los inicios de sesión en la PAL.  
  
#### <a name="to-add-groups-and-logins-to-the-pal"></a>Para agregar grupos e inicios de sesión a la PAL  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_grant_publication_access](/sql/relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql). En ** \@ publicación**, especifique el nombre de la publicación; y para ** \@ Inicio de sesión**, especifique el nombre del inicio de sesión o del grupo que se va a agregar.  
  
#### <a name="to-remove-groups-and-logins-from-the-pal"></a>Para quitar grupos e inicios de sesión de la PAL  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_revoke_publication_access](/sql/relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql). En ** \@ publicación**, especifique el nombre de la publicación; y para ** \@ Inicio de sesión**, especifique el nombre del inicio de sesión o del grupo que se va a quitar.  
  
## <a name="see-also"></a>Consulte también  
 [Modelo de seguridad del agente de replicación](replication-agent-security-model.md)   
 [Proteger una topología de replicación](view-and-modify-replication-security-settings.md)   
 [Proteger el publicador](secure-the-publisher.md)  
  
  
