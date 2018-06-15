---
title: Propiedades de la publicación, lista de acceso a la publicación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.publicationaccesslist.f1
ms.assetid: 9587bb9e-c66c-4e70-8171-09b943ec2d50
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f84b32e2d1a96d0416f1f5b8d6a73580a76af4ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32959772"
---
# <a name="publication-properties-publication-access-list"></a>Propiedades de la publicación, lista de acceso a la publicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La página **Lista de acceso a la publicación** del cuadro de diálogo **Propiedades de la publicación** permite agregar y quitar inicios de sesión, cuentas y grupos de la lista de acceso a la publicación (PAL). La PAL es el mecanismo principal para configurar la seguridad del publicador. Al crear una publicación, la replicación crea una PAL para dicha publicación. La PAL, que ofrece funciones similares a las de una lista de control de acceso de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, contiene una lista de inicios de sesión, cuentas y grupos con permiso de acceso a la publicación.  
  
 Cuando un suscriptor se conecta al publicador o al distribuidor y solicita acceso a la publicación, el inicio de sesión del suscriptor se compara con la información de autenticación de la PAL. Esto proporciona seguridad adicional para el publicador, ya que evita que en el inicio de sesión en el publicador o el distribuidor pueda usarse una herramienta cliente para realizar directamente modificaciones en el publicador. Para obtener más información, vea [Proteger el publicador](../../relational-databases/replication/security/secure-the-publisher.md).  
  
## <a name="options"></a>Opciones  
 **Agregar**  
 Permite agregar una nueva entrada a la lista. Puede agregar solo aquellos nombres de inicio de sesión, cuenta o grupo que ya estén definidos tanto en el publicador como en el distribuidor. Estarán definidos en ambos servidores si se usan cuentas de dominio o si se crean cuentas locales en ambos servidores.  
  
 **Quitar**  
 Permite quitar la entrada seleccionada de la lista.  
  
 **Quitar todo**  
 Quita todas las entradas de la lista.  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
