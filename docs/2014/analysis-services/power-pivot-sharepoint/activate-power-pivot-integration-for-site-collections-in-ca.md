---
title: Activar la integración de características de PowerPivot para colecciones de sitios en administración central | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5a8e3f2930d7975f8c75c8f89ab90b78461a650
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072007"
---
# <a name="activate-powerpivot-feature-integration-for-site-collections-in-central-administration"></a>Activar la integración de características de PowerPivot para colecciones de sitios en Administración central
  Activar la integración de características de PowerPivot para colecciones de sitios concretos es necesario si usó la opción de instalación Granja existente para instalar SQL Server PowerPivot para SharePoint. Si instaló PowerPivot para SharePoint con la opción Nuevo servidor, puede omitir esta tarea, porque el programa de instalación de SQL Server ya activó la integración de características de PowerPivot para la colección de sitios raíz al configurar la implementación.  
  
 La activación de características en el nivel de colección de sitios es necesario para que las plantillas y las páginas de las aplicaciones estén disponibles para los sitios, incluidas las páginas de configuración para la actualización de datos programada y las páginas de aplicación para las bibliotecas de Galería de PowerPivot y de fuentes de distribución de datos.  
  
 Debe activar la integración de PowerPivot para cada colección de sitios que admita el procesamiento de consultas de PowerPivot.  
  
## <a name="prerequisites"></a>Prerequisites  
 Debe ser administrador de la colección de sitios.  
  
## <a name="activate-powerpivot-features"></a>Activar las características de PowerPivot  
  
1.  En un sitio de SharePoint, haga clic en **Acciones de sitio**.  
  
     De forma predeterminada, se tiene acceso a las aplicaciones web de SharePoint a través del puerto 80. Esto significa que, a menudo, puede tener acceso a un sitio\<de SharePoint escribiendo http://nombre del equipo> para abrir la colección de sitios raíz.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  En Administración de la colección de sitios, haga clic en **Características de la colección de sitios**.  
  
4.  Desplácese hacia abajo en la página hasta que encuentre la **característica de colección de sitios de integración de PowerPivot**.  
  
5.  Haga clic en **Activar**.  
  
6.  Repita el procedimiento para las colecciones de sitios adicionales abriendo cada sitio y haciendo clic en **acciones del sitio**.  
  
## <a name="see-also"></a>Consulte también  
 [Administración y configuración del servidor de PowerPivot en administración central](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [PowerPivot para SharePoint de &#40;de configuración inicial&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
