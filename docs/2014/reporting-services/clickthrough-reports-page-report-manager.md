---
title: Informes Click-through página (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.drilthroughreports.f1
ms.assetid: e96cdeba-452b-45a8-9bcf-b75d76261e31
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: eb1c984abec2667a09587eda673ed02176aa8e8e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010578"
---
# <a name="clickthrough-reports-page-report-manager"></a>Página (Administrador de informes) Informes click-through
  Un informe click-through muestra una tabla de datos relacionados cuando se hace clic en los datos interactivos incluidos en el informe. El servidor de informes genera estos informes basándose en la información incluida en el modelo usado para crear el informe. Si no desea usar los informes click-through que el servidor de informes genera, puede crear informes personalizados que publica en un servidor de informes y asigna a los puntos de datos interactivos definidos en el modelo. Los informes personalizados se deben crear en el Generador de informes desde el mismo modelo y, a continuación, se deben publicar en el servidor de informes. Para asignar informes personalizados a los elementos del modelo, use la página Informes click-through en el Administrador de informes.  
  
 La página Informes click-through proporciona una manera de asignar los informes predefinidos y publicados del Generador de informes a las entidades, carpetas y elementos concretos dentro de un modelo. Cuando asigna un informe a un elemento dentro de un modelo, los usuarios que navegan a dicho elemento obtienen el informe personalizado en lugar de un informe temporal generado por el servidor de informes.  
  
 Si va a proporcionar informes personalizados, debería incluir una instancia única y una versión de varias instancias del informe. La ruta de acceso a datos por la que el usuario navega a una entidad específica determina si se presenta un informe de una sola instancia o de varias al usuario en tiempo de ejecución. No se puede saber siempre por anticipado si no se necesita una versión concreta del informe.  
  
 Los informes personalizados que asigna a entidades están protegidos en la jerarquía de carpetas del servidor de informes. Si se asigna un elemento de modelo a un informe, y dicho informe no está disponible para un usuario que ha navegado hasta él, el usuario obtendrá un informe temporal generado por el servidor de informes en lugar del informe que se diseñó.  
  
 Aunque puede seleccionar cualquier informe al que tenga acceso, seleccione solo los creados específicamente para el modelo que está configurando.  
  
> [!NOTE]  
>  Los informes click-through no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Si no está seguro de la edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la que trabaja su organización, póngase en contacto con el administrador de la base de datos.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-clickthrough-reports-page"></a>Para abrir la página Informes click-through  
  
1.  Abra el Administrador de informes y busque el modelo a cuyas entidades desea asignar los informes click-through.  
  
2.  Mantenga el mouse sobre el modelo y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades **General** correspondiente al modelo.  
  
4.  Seleccione la pestaña **Click-through** .  
  
## <a name="options"></a>Opciones  
 **Jerarquía de elementos de modelo**  
 Muestra las entidades, las carpetas y los elementos del espacio de nombres de modelo para el que puede proporcionar un informe personalizado.  
  
 **Informe de instancia única**  
 Especifica el informe personalizado que se va a utilizar cuando la navegación del usuario requiere una vista de datos de instancia única. Haga clic en el botón Examinar para seleccionar el informe que desea utilizar.  
  
 **Informe de varias instancias**  
 Especifica el informe personalizado que se va a utilizar cuando la navegación del usuario requiere una vista de datos de varias instancias. Haga clic en el botón Examinar para seleccionar el informe que desea utilizar.  
  
## <a name="see-also"></a>Vea también  
 [Publicar informes](../../2014/reporting-services/publish-reports.md)  
  
  
