---
description: Contraseña del distribuidor
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 6593e4065e4ea40f0befb7bb236db5c99a54461e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484877"
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
  
  
