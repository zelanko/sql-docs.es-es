---
title: Carpeta de instantáneas | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 48b490c65662edf65018e98dd1bc3339f6aae6b6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055621"
---
# <a name="snapshot-folder"></a>Carpeta de instantáneas
  La página **Carpeta de instantáneas** aparece en el Asistente para configurar la distribución y en el Asistente para nueva publicación. La ubicación que se especifique para la carpeta de instantáneas se utilizará como la predeterminada para todos los publicadores habilitados en este asistente (la carpeta de instantáneas predeterminada no se aplica a los publicadores que se habilitan posteriormente mediante el cuadro de diálogo **Propiedades del distribuidor** ). Puede sobrescribir este valor predeterminado en cualquier publicador de la página **Publicadores** del Asistente para configurar la distribución o el cuadro de diálogo **Propiedades del distribuidor** .  
  
 La carpeta de instantáneas es simplemente un directorio designado como recurso compartido; los agentes que leen y escriben en esta carpeta deben tener permisos de acceso suficientes a ella. Para obtener más información sobre cómo proteger la carpeta adecuadamente, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md). Antes de implementar la replicación, compruebe que los agentes de replicación podrán conectarse a la carpeta de instantáneas. Inicie la sesión con la cuenta que utilizará cada agente y, a continuación, intente tener acceso a la carpeta de instantáneas.  
  
## <a name="options"></a>Opciones  
 **Carpeta de instantáneas**  
 Escriba la ruta de acceso de la carpeta donde desea almacenar los archivos de instantáneas.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda utilizar un recurso de red compartido como ubicación para la carpeta de instantáneas. Los agentes en otros equipos no tienen acceso a las rutas de acceso locales (las que empiezan con una letra de unidad como C:\\).  
  
## <a name="see-also"></a>Consulte también  
 [Ubicaciones de carpeta de instantáneas alternativas](alternate-snapshot-folder-locations.md)   
 [Configurar la distribución](configure-distribution.md)   
 [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)  
  
  
