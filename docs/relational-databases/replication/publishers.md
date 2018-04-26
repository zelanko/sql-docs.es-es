---
title: Publicadores | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.configuredistributionwizard.enablepublishers.f1
ms.assetid: 116cd6a5-32ac-4273-81a2-d184408e0f07
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 57f8b96e4d29b045a54bae7fe2d4411457fb8d2a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="publishers"></a>Publicadores
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede otorgar permisos para que otros publicadores utilicen este distribuidor. Tenga en cuenta que permitir que un publicador utilice este servidor como su distribuidor remoto no hace que ese servidor sea un publicador. Debe conectarse al publicador, configurarlo para publicación y elegir este servidor como el distribuidor. Con el Asistente para nueva publicación puede configurar el publicador y elegir un distribuidor.  
  
 Los servidores que seleccione como publicadores utilizarán la base de datos de distribución especificada en la página **Base de datos de distribución** de este asistente. Si desea utilizar una base de datos de distribución diferente, no habilite el publicador en este momento. En lugar de ello, utilice el cuadro de diálogo **Propiedades del distribuidor** para agregar los publicadores una vez que haya finalizado el Asistente para configurar la distribución.  
  
## <a name="options"></a>Opciones  
 **Publicadores**  
 Seleccione los servidores que pueden utilizar este distribuidor. Haga clic en el botón (**...**) de propiedades que se encuentra junto a un publicador para ver y establecer propiedades adicionales.  
  
 **Agregar**  
 Si el servidor que desea habilitar no aparece, haga clic en **Agregar** para agregar un publicador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un publicador de Oracle a la lista de publicadores disponibles.  
  
## <a name="see-also"></a>Ver también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
