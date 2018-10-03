---
title: Propiedades del distribuidor, Publicadores | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distproperties.publishers.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: 31c81898-11ca-4d2f-afea-2fbc71e19ce4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3c8f572b45154b76f711ab61fe35be339429ed83
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123715"
---
# <a name="distributor-properties-publishers"></a>Propiedades del distribuidor, Publicadores
  La página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor** permite habilitar a los publicadores para que puedan utilizar este distribuidor. También se pueden establecer propiedades asociadas con esos publicadores. Tenga en cuenta que permitir que un publicador utilice este servidor como su distribuidor remoto no hace que ese servidor sea un publicador. Debe conectarse al publicador, configurarlo para publicación y elegir este servidor como el distribuidor. Con el Asistente para nueva publicación puede configurar el publicador y elegir un distribuidor.  
  
## <a name="options"></a>Opciones  
 **Publicadores**  
 Seleccione los servidores que pueden utilizar este distribuidor. Haga clic en el botón **(...)** de Propiedades que se encuentra junto a un publicador para ver y establecer propiedades adicionales.  
  
 **Agregar**  
 Si el servidor que desea habilitar no aparece, haga clic en **Agregar** para agregar un publicador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un publicador de Oracle a la lista de publicadores disponibles. Si el servidor que agrega es el primer servidor que utilizará este distribuidor como distribuidor remoto, se le solicitará que proporcione una contraseña de vínculo administrativo.  
  
 **Contraseña de vínculo administrativo**  
 Use esta opción para especificar o actualizar la contraseña para la conexión que hace la replicación entre el publicador y el distribuidor remoto con el inicio de sesión **distributor_admin** :  
  
-   Si el distribuidor solo sirve a un distribuidor local, esta contraseña se genera de forma aleatoria y se configura automáticamente.  
  
-   Si el distribuidor ya tiene un publicador remoto, ello indica que inicialmente se ha suministrado una contraseña en esta página o en la página **Contraseña del distribuidor** del Asistente para configurar la distribución.  
  
-   Si habilita el primer publicador remoto para este distribuidor, se le solicitará que escriba una contraseña.  
  
 Para más información acerca de la seguridad para Distribuidores, vea [Proteger el distribuidor](security/secure-the-distributor.md).  
  
## <a name="see-also"></a>Vea también  
 [Configurar distribución](configure-distribution.md)   
 [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)  
  
  
