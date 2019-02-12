---
title: Nuevo rol del sistema (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.newsystemrole.f1
ms.assetid: 7b4a0b98-975b-478a-8359-7db39ccbb347
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 44d0318882b619f4f6206f59ba47656f35c38636
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043366"
---
# <a name="new-system-role-management-studio"></a>Nuevo rol del sistema (Management Studio)
  Utilice esta página para crear una definición de roles de nivel del sistema. Una definición de roles del sistema especifica un conjunto de tareas de nivel de sistema que se aplican a un servidor de informes como un conjunto.  
  
> [!NOTE]  
>  Las definiciones de roles solo se utilizan en un servidor de informes que se ejecute en modo nativo. Si el servidor de informes está configurado para la integración con SharePoint, esta página no está disponible.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba el nombre de la definición de roles. Un nombre de definición de roles debe ser único en el espacio de nombres del servidor de informes. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios y algunos símbolos. No utilice los caracteres siguientes al especificar un nombre:  
  
 ; ? : \@ & = + , $ / * \< >  
  
 " /  
  
 **Descripción**  
 Proporcione una descripción que explique cómo usar el rol y que indique lo que admite.  
  
 **Tarea**  
 Seleccione las tareas de nivel de sistema que se pueden realizar mediante este rol. No puede crear nuevas tareas ni modificar las tareas existentes que admite [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. No puede elegir tareas de nivel de elemento para una definición de rol del sistema.  
  
 **Descripción de la tarea**  
 Muestra una descripción de la tarea con las operaciones o los permisos que ésta admite.  
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)   
 [Definiciones de roles](../security/role-definitions.md)  
  
  
