---
title: Propiedades del publicador, cuadro de diálogo (SSMS)
description: Describe el cuadro de diálogo "Propiedades del publicador" para una publicación específica en SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.distpubproperties.f1
- sql13.rep.configdistwizard.pubproperties.general.f1
- sql13.rep.configdistwizard.pubproperties.pubdb.f1
- sql13.rep.configdistwizard.pubproperties.subscribers.f1
ms.assetid: 98df1aea-0406-40bf-a917-4bd80464125c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2af128ab6de902aa7e757cf9d7464c9b743c290b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717640"
---
# <a name="sql-server-replication-publisher-properties-dialog-box"></a>Cuadro de diálogo Propiedades del publicador de Replicación de SQL Server
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

En este tema se describen las distintas opciones del cuadro de diálogo Propiedades del publicador. 

## <a name="general"></a>General
  La página **General** del cuadro de diálogo **Propiedades del publicador** muestra información de solo lectura sobre el distribuidor y la base de datos de distribución usada por el publicador. Para cambiar el distribuidor o la base de datos de distribución de un publicador:  
  
1.  Deshabilite la publicación en el publicador. Para obtener más información, vea [Deshabilitar la publicación y distribución](../../relational-databases/replication/disable-publishing-and-distribution.md).    
2.  Vuelva a configurar la publicación y la distribución. Para obtener más información, consulte [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md).  

## <a name="distributor"></a>Distribuidor. 
El cuadro de diálogo **Propiedades del publicador** le permitirá ver y modificar las propiedades asociadas a la relación entre el publicador y el distribuidor.  
  
### <a name="options"></a>Opciones  
 **Conexión del agente al publicador**  
 Especifique el contexto en el que los siguientes agentes establecerán conexiones del distribuidor al publicador:  
  
-   Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones de actualización en cola    
-   Agente de instantáneas y Agente de registro del LOG para publicaciones de Oracle  
  
 Seleccione **Suplantar cuenta de proceso del agente** para establecer conexiones al publicador a través del contexto de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecutan los agentes o especifique **Autenticación de SQL Server**y escriba un valor para **Inicio de sesión** y **Contraseña**. Se recomienda seleccionar **Suplantar cuenta de proceso del agente**. Para obtener más información, vea [Modelo de seguridad del agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Las cuentas de Windows con las que se ejecutan los agentes se especifican en el Asistente para nueva publicación. Podrá cambiar las cuentas:  
  
-   En el cuadro de diálogo **Propiedades del distribuidor** del Agente de lectura de cola.    
-   En el cuadro de diálogo **Propiedades de la publicación** del Agente de instantáneas y del Agente de registro del LOG.  
  
 **Varios**  
 Las propiedades **Tipo de publicador** y **Nombre de base de datos de distribución** son de solo lectura. Es posible cambiar la propiedad **Carpeta de instantáneas predeterminada** . Para obtener más información sobre la carpeta de instantáneas, vea [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  

## <a name="publication-databases"></a>Bases de datos de publicación
  La página **Bases de datos de publicaciones** del cuadro de diálogo **Propiedades del publicador** permite a un usuario que tenga el rol fijo de servidor **sysadmin** habilitar bases de datos para replicación. Al habilitar una base de datos, ésta no se publica, sino que permite que cualquier usuario del rol fijo de base de datos **db_owner** para esa base de datos cree una o varias publicaciones en la base de datos.  
  
## <a name="options"></a>Opciones  
 **Transaccional**  
 Active esta casilla para permitir que los usuarios que tengan el rol fijo de base de datos **db_owner** creen publicaciones de instantáneas o publicaciones transaccionales en la base de datos. 
  
 **Combinar**  
 Active esta casilla para permitir que los usuarios que tengan el rol fijo de base de datos **db_owner** creen publicaciones de combinación en la base de datos.  
  

## <a name="subcribers"></a>Suscriptores
  La página **Suscriptores** del cuadro de diálogo **Propiedades del publicador** se utiliza para que los publicadores ejecuten versiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Esta página permite habilitar a los suscriptores para que reciban datos de publicaciones de este Publicador. Al habilitar un suscriptor para que reciba de desde este Publicador no se crean suscripciones para publicaciones de este publicador. Para crear una suscripción, debe utilizar el Asistente para nueva suscripción.  
  
### <a name="options"></a>Opciones  
 **Suscriptores**  
 La cuadrícula de propiedades de **Suscriptores** muestra los suscriptores que están habilitados para recibir datos de las publicaciones de este publicador. Haga clic en el botón de propiedades ( **...** ) que se encuentra junto a un suscriptor para ver y establecer propiedades adicionales.  
  
 **Add (Agregar)**  
 Haga clic en **Agregar** para agregar un suscriptor, y luego haga clic en **Agregar suscriptor de SQL Server** o en **Agregar suscriptor que no sea de SQL Server**.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md) (Creación de una publicación)   


  
