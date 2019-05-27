---
title: Habilitar y deshabilitar Mis informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deactivated My Reports folder
- folders [Reporting Services], My Reports
- activated My Reports folder
- My Reports folder [Reporting Services]
- disabling My Reports folder
ms.assetid: 16c76e82-9fd4-417c-9ed3-a7d5bcd1dba2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eba2db61acb691732f81dcd0fa98b0ba48cf921e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103849"
---
# <a name="enable-and-disable-my-reports"></a>Habilitar y deshabilitar Mis informes
  La característica Mis informes asigna espacio de almacenamiento personal en la base de datos del servidor de informes para que los usuarios puedan guardar sus propios informes en una carpeta privada. Los administradores de servidores de informes pueden habilitar o deshabilitar esta característica o cambiar su funcionamiento modificando la configuración de seguridad que controla las acciones que los usuarios llevan a cabo en esta área de trabajo.  
  
 La característica Mis informes se deshabilita de manera predeterminada. Existe la posibilidad de habilitarla o deshabilitarla para todos los usuarios, pero no se puede habilitar para un subconjunto de usuarios. Esta característica resulta útil para la mayoría de los usuarios y las organizaciones. Sopese las ventajas y los inconvenientes que se describen más adelante en este mismo tema para determinar si se trata de una buena elección para su organización.  
  
## <a name="how-to-enable-and-disable-my-reports"></a>Habilitar y deshabilitar Mis informes  
 Para habilitar Mis informes con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia del servidor de informes y abra la página **Propiedades del servidor** . Después, en la pestaña **General** , seleccione la opción **Habilitar una carpeta Mis informes para cada usuario** .  
  
 La definición de roles empleada para Mis informes determinará las acciones admitidas en el área de trabajo Mis informes. Por ejemplo, si el rol Mis informes excluye "Crear informes vinculados", los usuarios no podrán crear informes vinculados en las carpetas Mis informes. Para más información, vea [Proteger Mis informes](../security/secure-my-reports.md).  
  
 Para desactivar Mis informes, desactive la opción **Habilitar una carpeta Mis informes para cada usuario**. Al desactivar la característica Mis informes, se quitan todas las indicaciones visibles para los usuarios de la carpeta Mis informes. Las carpetas que ofrecen almacenamiento real (es decir, las subcarpetas de Carpetas de usuarios) deben eliminarse manualmente tras deshabilitar la característica.  
  
### <a name="when-my-reports-is-activated"></a>Cuando la característica Mis informes está activada  
 Cuando la característica está activada, los usuarios ven una carpeta Mis informes que se encuentra debajo de la carpeta raíz Inicio. Además de esta carpeta, los administradores del servidor de informes también pueden ver una carpeta denominada Carpetas de usuarios que contiene una subcarpeta para cada usuario.  
  
 Mientras la característica está activada no pueden eliminarse ni la carpeta Carpetas de usuarios ni sus subcarpetas. Por otra parte, el nombre "Mis informes" pasa a ser un nombre reservado para las carpetas que se creen en el nodo raíz (Inicio).  
  
 Si activa Mis informes después de haber desactivado la característica, el servidor de informes creará una nueva carpeta Carpetas de usuarios si no existe ninguna. Si ya existe, el servidor de informes agregará subcarpetas nuevas conforme los usuarios se conecten a sus carpetas Mis informes.  
  
### <a name="when-my-reports-is-deactivated"></a>Cuando la característica Mis informes está desactivada  
 Una vez desactivada la característica, el nombre "Mis informes" deja de estar reservado, por lo que los usuarios pueden crear carpetas personales denominadas Mis informes en la carpeta Inicio. Además, ya no se permite la redirección de Mis informes a subcarpetas de Mis informes específicas del usuario. Por último, los vínculos de informe que incluyan una carpeta Mis informes específica del usuario en la dirección URL ya no funcionarán.  
  
## <a name="choosing-to-use-my-reports"></a>Optar por usar Mis informes  
 La decisión de optar por utilizar Mis informes depende de si se desean dedicar recursos del servidor para el área de trabajo de un usuario. Mis informes es una característica muy eficaz que permite a los usuarios controlar los recursos de información que les ayudan a realizar sus trabajos. También es un modo de que los usuarios puedan trabajar con los informes no concebidos para uso general. Uno de los motivos decisivos para utilizar Mis informes es la compatibilidad segura y administrable para un segmento de usuarios que precisan crear y revisar informes. Sin esta característica es probable que se encuentre creando carpetas y directivas de seguridad para distintos usuarios cada vez que la situación lo requiera. Dado que tanto los usuarios como sus necesidades evolucionan, este enfoque da lugar a un número cada vez mayor de carpetas y directivas que con el paso del tiempo resultan difíciles de mantener.  
  
 Tenga en cuenta que, si activa Mis informes, el servidor de informes creará una carpeta Mis informes para cada usuario que tenga una cuenta de dominio y que haga clic en el vínculo Mis informes, incluso si el usuario no desea, o no necesita, una carpeta Mis informes. No existe ningún modo sistemático de determinar las carpetas que se utilizan. Es preciso revisar manualmente las carpetas para comprobar las que contienen algo.  
  
## <a name="see-also"></a>Vea también  
 [Proteger Mis informes](../security/secure-my-reports.md)   
 [Administración de contenido del servidor de informes &#40;Modo nativo de SSRS&#41;](report-server-content-management-ssrs-native-mode.md)  
  
  
