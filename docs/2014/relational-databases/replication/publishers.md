---
title: Publicadores | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.enablepublishers.f1
ms.assetid: 116cd6a5-32ac-4273-81a2-d184408e0f07
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3b28a0543208ab28414fb93def15adf904e2c078
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63261728"
---
# <a name="publishers"></a>Publicadores
  Puede otorgar permisos para que otros publicadores utilicen este distribuidor. Tenga en cuenta que permitir que un publicador utilice este servidor como su distribuidor remoto no hace que ese servidor sea un publicador. Debe conectarse al publicador, configurarlo para publicación y elegir este servidor como el distribuidor. Con el Asistente para nueva publicación puede configurar el publicador y elegir un distribuidor.  
  
 Los servidores que seleccione como publicadores utilizarán la base de datos de distribución especificada en la página **Base de datos de distribución** de este asistente. Si desea utilizar una base de datos de distribución diferente, no habilite el publicador en este momento. En lugar de ello, utilice el cuadro de diálogo **Propiedades del distribuidor** para agregar los publicadores una vez que haya finalizado el Asistente para configurar la distribución.  
  
## <a name="options"></a>Opciones  
 **Publicadores**  
 Seleccione los servidores que pueden utilizar este distribuidor. Haga clic en el botón ( **...** ) de propiedades que se encuentra junto a un publicador para ver y establecer propiedades adicionales.  
  
 **Add (Agregar)**  
 Si el servidor que quiere habilitar no aparece, haga clic en **Agregar** para agregar un publicador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un publicador de Oracle a la lista de publicadores disponibles.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar distribución](configure-distribution.md)   
 [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [Create a Publication](publish/create-a-publication.md) (Creación de una publicación)  
  
  
