---
title: Programa de página (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ef19d96e-9f00-4434-950e-152dda9c1ced
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3dc1cfa85fde084327567e36fea728d9c76ef3f6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028256"
---
# <a name="schedules-page-report-manager"></a>Página de Programaciones (Administrador de informes)
  Use la página Programaciones para crear, modificar, eliminar, pausar o reanudar programaciones compartidas. Una programación compartida es una programación con nombre que se puede crear y administrar independientemente de los informes, las suscripciones y los demás procesos que utilizan información de programación. Los usuarios pueden seleccionar las programaciones compartidas que proporcione.  
  
 Para eliminar, pausar o reanudar una programación compartida, active la casilla que se encuentra junto a la programación compartida que desea modificar.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-schedules-page"></a>Para abrir la página Programaciones  
  
1.  Abra el Administrador de informes.  
  
2.  En la esquina superior derecha, haga clic en **Configuración del sitio**. Esto abre la página de propiedades General del sitio.  
  
3.  Seleccione la pestaña **Programaciones** .  
  
## <a name="options"></a>Opciones  
 **Nueva programación**  
 Haga clic para abrir la página Programación, que se usa para especificar información de frecuencia.  
  
 **Eliminar**  
 Haga clic para quitar una programación compartida.  
  
 **Pausar**  
 Haga clic para impedir que una programación compartida se ejecute temporalmente. Al pausar una programación, se impide la ejecución de suscripciones y otros procesos programados.  
  
 **Reanudar**  
 Haga clic para restablecer una programación compartida. Los procesos que estaban programados para ejecutarse mientras la programación estaba pausada no se completan.  
  
 **Programación**  
 Muestra las programaciones compartidas actualmente definidas. Haga clic en una programación compartida para ver o editar la información de frecuencia.  
  
 **Creador**  
 Muestra el nombre del usuario que creó la programación compartida.  
  
 **Última ejecución, siguiente ejecución**  
 Muestran cuándo se ejecutó la programación compartida por última vez y cuándo se volverá a ejecutar.  
  
 **Estado**  
 Indica si una programación compartida está en pausa o activa.  
  
## <a name="see-also"></a>Vea también  
 [Crear, modificar y eliminar programaciones](subscriptions/create-modify-and-delete-schedules.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
