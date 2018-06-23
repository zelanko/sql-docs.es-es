---
title: Propiedades de Analysis Server (pestaña iniciar sesión) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a82e0c98-efaa-4b0b-9582-3c879ee42444
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2687a9e046529927f694b8da0d0d8f11bfccf7f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108006"
---
# <a name="analysis-server-properties-log-on-tab"></a>Propiedades de Analysis Server (pestaña Iniciar sesión)
  Utilice la pestaña **Iniciar sesión** del cuadro de diálogo **Propiedades de Analysis Server** para especificar la cuenta que utiliza el servicio [!INCLUDE[ssAS](../../includes/ssas-md.md)] así como para iniciar y detener el servicio.  
  
> [!NOTE]  
>  Cuando cambie el **Nombre de cuenta** utilizado por un servicio en una instancia en clúster, la nueva cuenta debe formar parte del grupo de dominios que haya especificado durante la instalación del servicio modificado, o bien debe tener permiso para agregar miembros a ese grupo. Si no tiene permisos para modificar la pertenencia al grupo, póngase en contacto con el administrador del dominio.  
  
## <a name="options"></a>Opciones  
 **Cuenta de sistema local**  
 Especifique una cuenta de sistema local, que no requiere una contraseña. No obstante, la cuenta del sistema local puede restringir la interacción del servicio con otros servidores, en función de los privilegios que se le hayan concedido.  
  
 **Esta cuenta**  
 Especifique una cuenta de usuario local o de dominio que utilice la autenticación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda utilizar una cuenta de usuario de dominio que tenga derechos mínimos para los servicios. Para obtener información acerca de cómo seleccionar una cuenta, busque el tema sobre cómo configurar cuentas de servicios de Windows en los Libros en pantalla.  
  
 **Nombre de cuenta**  
 Escriba el nombre de la cuenta de usuario local o de dominio.  
  
 **Contraseña**  
 Escriba la contraseña de la cuenta.  
  
 **Confirmar contraseña**  
 Escriba de nuevo la contraseña de la cuenta.  
  
 **Iniciar**  
 Inicie el servicio.  
  
 **Detener**  
 Detenga el servicio.  
  
 **Pausar**  
 Pause el servicio.  
  
 **Reanudar**  
 Reanude un servicio en pausa.  
  
  