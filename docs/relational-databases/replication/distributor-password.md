---
title: Contraseña del distribuidor | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 76143a4158aab90a96b015566bc993a7f70ef0d8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85653385"
---
# <a name="distributor-password"></a>Contraseña del distribuidor
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Si, en la página **Publicadores** de este asistente, habilitó uno o varios Publicadores para que utilizaran este servidor como Distribuidor remoto, debe especificar una contraseña para la conexión que la replicación realiza entre el Publicador y el Distribuidor remoto, utilizando el inicio de sesión **distributor_admin** . Se debe especificar la misma contraseña para cada Publicador que utiliza este Distribuidor remoto en la página **Contraseña administrativa** del Asistente para nueva publicación o del Asistente para configurar la distribución. Para más información acerca de la seguridad para Distribuidores, vea [Proteger el distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## <a name="options"></a>Opciones  
 **Contraseña**  
 Escriba una contraseña segura para la conexión entre el Publicador y el Distribuidor remoto.  
  
 **Confirm Password**  
 Vuelva a escribir la contraseña para confirmar que es correcta.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
