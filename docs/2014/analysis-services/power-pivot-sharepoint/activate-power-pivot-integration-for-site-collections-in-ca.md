---
title: Activar la integración de características de PowerPivot para colecciones de sitios en Administración Central | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 00e8f0336c075c14feb8c4e3b4a8b43e0ebdaf9e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198544"
---
# <a name="activate-powerpivot-feature-integration-for-site-collections-in-central-administration"></a>Activar la integración de características de PowerPivot para colecciones de sitios en Administración central
  Activar la integración de características de PowerPivot para colecciones de sitios concretos es necesario si usó la opción de instalación Granja existente para instalar SQL Server PowerPivot para SharePoint. Si instaló PowerPivot para SharePoint con la opción Nuevo servidor, puede omitir esta tarea, porque el programa de instalación de SQL Server ya activó la integración de características de PowerPivot para la colección de sitios raíz al configurar la implementación.  
  
 La activación de características en el nivel de colección de sitios es necesario para que las plantillas y las páginas de las aplicaciones estén disponibles para los sitios, incluidas las páginas de configuración para la actualización de datos programada y las páginas de aplicación para las bibliotecas de Galería de PowerPivot y de fuentes de distribución de datos.  
  
 Debe activar la integración de PowerPivot para cada colección de sitios que admita el procesamiento de consultas de PowerPivot.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Debe ser administrador de la colección de sitios.  
  
## <a name="activate-powerpivot-features"></a>Activar las características de PowerPivot  
  
1.  En un sitio de SharePoint, haga clic en **Acciones de sitio**.  
  
     De forma predeterminada, se tiene acceso a las aplicaciones web de SharePoint a través del puerto 80. Esto significa que puede acceder a menudo un sitio de SharePoint escribiendo http://\<nombre de equipo > para abrir la colección de sitios raíz.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  En Administración de la colección de sitios, haga clic en **Características de la colección de sitios**.  
  
4.  Desplácese hacia abajo en la página hasta que encuentre **característica de colección de sitios de integración de PowerPivot**.  
  
5.  Haga clic en **Activar**.  
  
6.  Repita este procedimiento con las demás colecciones de sitios abriendo cada sitio y haciendo clic en **Acciones de sitio**.  
  
## <a name="see-also"></a>Vea también  
 [Administración de servidor de PowerPivot y configuración en Administración Central](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configuración inicial &#40;PowerPivot para SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot para SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  