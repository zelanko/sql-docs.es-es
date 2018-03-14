---
title: "Especificar el formato de instantánea (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5bae3f755eaca45f2388a7d855a8c034cc5901a
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>Especificar el formato de instantánea (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifique el formato de instantánea en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Para especificar el formato de instantánea  
  
1.  En la página **Instantánea**, del cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione **SQL Server nativo: todos los suscriptores deben ser servidores que ejecuten SQL Server** o **Carácter: es necesario si un publicador o suscriptor no ejecuta SQL Server**.  
  
    > [!NOTE]  
    >  Se recomienda seleccionar el formato nativo, a menos que esta publicación deba ser compatible con suscripciones a una base de datos de [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o una base de datos que no sea de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
