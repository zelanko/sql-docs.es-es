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
ms.openlocfilehash: 53605b1e88c47c5fa9b2f0ee37147993e0375808
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "76284010"
---
# <a name="distributor-password"></a>Contraseña del distribuidor
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Si, en la página **Publicadores** de este asistente, habilitó uno o varios Publicadores para que utilizaran este servidor como Distribuidor remoto, debe especificar una contraseña para la conexión que la replicación realiza entre el Publicador y el Distribuidor remoto, utilizando el inicio de sesión **distributor_admin** . Se debe especificar la misma contraseña para cada Publicador que utiliza este Distribuidor remoto en la página **Contraseña administrativa** del Asistente para nueva publicación o del Asistente para configurar la distribución. Para más información acerca de la seguridad para Distribuidores, vea [Proteger el distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## <a name="options"></a>Opciones  
 **Contraseña**  
 Escriba una contraseña segura para la conexión entre el Publicador y el Distribuidor remoto.  
  
 **Confirm Password**  
 Vuelva a escribir la contraseña para confirmar que es correcta.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
