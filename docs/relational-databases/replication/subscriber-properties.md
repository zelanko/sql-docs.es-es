---
description: Propiedades del suscriptor
title: Propiedades del suscriptor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 366740d950e249d6ad18e97af3094208d4d849fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493902"
---
# <a name="subscriber-properties"></a>Propiedades del suscriptor
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  El cuadro de diálogo **Propiedades del suscriptor** contiene información relevante para los suscriptores que ejecutan versiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a la [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]

  
## <a name="options"></a>Opciones  
 **Conexión del agente al suscriptor**  
 Contexto bajo el que el Agente de distribución y el Agente de mezcla conectan desde el distribuidor al suscriptor. Se aplica solamente a versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Seleccione **Suplantar cuenta de proceso del agente** para establecer conexiones al suscriptor a través del contexto de la cuenta del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el distribuidor, o especifique **Autenticación de SQL Server**y escriba un valor para **Inicio de sesión** y **Contraseña**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que se seleccione **Suplantar cuenta de proceso del agente**.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores la información de conexión se especifica para cada suscripción en el Asistente para nueva suscripción y puede cambiar en el cuadro de diálogo **Propiedades de suscripción** .  
  
 **Programaciones predeterminadas del agente**  
 Programación predeterminada utilizada en el Asistente para nueva suscripción para suscriptores que ejecutan versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 **Varios**  
 Incluye información sobre el suscriptor y el tipo de suscriptor.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
