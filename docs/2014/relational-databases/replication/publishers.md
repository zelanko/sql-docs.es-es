---
title: Publicadores | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.enablepublishers.f1
ms.assetid: 116cd6a5-32ac-4273-81a2-d184408e0f07
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df92a2632047ae23c15973806848ac824f982818
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096495"
---
# <a name="publishers"></a>Publicadores
  Puede otorgar permisos para que otros publicadores utilicen este distribuidor. Tenga en cuenta que permitir que un publicador utilice este servidor como su distribuidor remoto no hace que ese servidor sea un publicador. Debe conectarse al publicador, configurarlo para publicación y elegir este servidor como el distribuidor. Con el Asistente para nueva publicación puede configurar el publicador y elegir un distribuidor.  
  
 Los servidores que seleccione como publicadores utilizarán la base de datos de distribución especificada en la página **Base de datos de distribución** de este asistente. Si desea utilizar una base de datos de distribución diferente, no habilite el publicador en este momento. En lugar de ello, utilice el cuadro de diálogo **Propiedades del distribuidor** para agregar los publicadores una vez que haya finalizado el Asistente para configurar la distribución.  
  
## <a name="options"></a>Opciones  
 **Publicadores**  
 Seleccione los servidores que pueden utilizar este distribuidor. Haga clic en el botón (**...**) de propiedades que se encuentra junto a un publicador para ver y establecer propiedades adicionales.  
  
 **Agregar**  
 Si el servidor que desea habilitar no aparece, haga clic en **Agregar** para agregar un publicador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un publicador de Oracle a la lista de publicadores disponibles.  
  
## <a name="see-also"></a>Vea también  
 [Configurar distribución](configure-distribution.md)   
 [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [Crear una publicación](publish/create-a-publication.md)  
  
  
