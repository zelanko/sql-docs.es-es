---
title: Habilitar un publicador remoto en un distribuidor (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote Distributors [SQL Server replication]
- Publishers [SQL Server replication]
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 848c1142c1db178efe9215db06fd326ea4aade6e
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="enable-a-remote-publisher-at-a-distributor-sql-server-management-studio"></a>Habilitar un publicador remoto en un distribuidor (SQL Server Management Studio)
  Habilite un publicador para utilizar un distribuidor remoto en la página **Publicadores** . Esta página está disponible en el Asistente para configurar la distribución y en el cuadro de diálogo **Propiedades del distribuidor: \<Distribuidor>**. Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, consulte [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md) y [Ver y modificar propiedades del distribuidor y el publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-enable-a-publisher-in-the-configure-distribution-wizard"></a>Para habilitar un publicador en el Asistente para configurar la distribución  
  
1.  En la página **Publicadores** del Asistente para configurar la distribución, haga clic en **Agregar**.  
  
2.  Haga clic en **Agregar publicador de SQL Server**. Para obtener información acerca de cómo habilitar un publicador de Oracle para utilizar un distribuidor, vea [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  En el cuadro de diálogo **Conectar al servidor** , especifique la información de conexión con el publicador que utilizará el distribuidor remoto y, a continuación, haga clic en **Conectar**.  
  
4.  En la página **Contraseña del distribuidor** , en los cuadros de texto **Contraseña** y **Confirmar contraseña** , especifique una contraseña segura para la cuenta **distributor_admin** , que la replicación utiliza para conectar del publicador al distribuidor y realizar las tareas administrativas.  
  
5.  Para ver y modificar la configuración de un publicador, haga clic en el botón de propiedades (**…**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-enable-a-publisher-in-the-distributor-properties-dialog-box"></a>Para habilitar un publicador en el cuadro de diálogo Propiedades del distribuidor  
  
1.  En la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor: \<Distribuidor>**, haga clic en **Agregar**.  
  
2.  Haga clic en **Agregar publicador de SQL Server**. Para obtener información acerca de cómo habilitar un publicador de Oracle para utilizar un distribuidor, vea [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  En el cuadro de diálogo **Conectar al servidor** , especifique la información de conexión con el publicador que utilizará el distribuidor remoto y, a continuación, haga clic en **Conectar**.  
  
4.  En la página **Publicadores** , en los cuadros de texto **Contraseña** y **Confirmar contraseña** , especifique una contraseña segura para la cuenta **distributor_admin** , que la replicación utiliza para conectar del publicador al distribuidor y realizar las tareas administrativas.  
  
5.  Para ver y modificar la configuración de un publicador, haga clic en el botón de propiedades (**…**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Proteger el distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
