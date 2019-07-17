---
title: Activar la integración de PowerPivot para colecciones de sitios en la entidad emisora de certificados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 564ff616ec13b5f7f669db4cf6402114175f5670
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164467"
---
# <a name="activate-power-pivot-integration-for-site-collections-in-ca"></a>Activar la integración de PowerPivot para colecciones de sitios en la entidad de certificación
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Es necesario activar la integración de características de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para colecciones de sitios concretos si se ha usado la opción de instalación Granja existente para instalar SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Si ha instalado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint con la opción Nuevo servidor, puede omitir esta tarea, porque el programa de instalación de SQL Server ya ha activado la integración de características de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para la colección de sitios raíz al configurar la implementación.  
  
 Es necesario activar las características en el nivel de colección de sitios para que las plantillas y las páginas de las aplicaciones estén disponibles para los sitios, incluidas las páginas de configuración para la actualización de datos programada y las páginas de aplicación para las bibliotecas de Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y de fuentes de distribución de datos.  
  
 Debe activar la integración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para cada colección de sitios que admita el procesamiento de consultas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## <a name="prerequisites"></a>Requisitos previos  
 Debe ser administrador de la colección de sitios.  
  
## <a name="activate-power-pivot-features"></a>Activar las características de PowerPivot  
  
1.  En un sitio de SharePoint, haga clic en **Acciones de sitio**.  
  
     De forma predeterminada, se tiene acceso a las aplicaciones web de SharePoint a través del puerto 80. Esto significa que puede acceder a menudo un sitio de SharePoint escribiendo http://\<nombre_equipo > para abrir la colección de sitios raíz.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  En Administración de la colección de sitios, haga clic en **Características de la colección de sitios**.  
  
4.  Desplácese hacia abajo en la página hasta que encuentre **Característica de colección de sitios de integración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** .  
  
5.  Haga clic en **Activar**.  
  
6.  Repita este procedimiento con las demás colecciones de sitios abriendo cada sitio y haciendo clic en **Acciones de sitio**.  
  
## <a name="see-also"></a>Vea también  
 [Administración y configuración del servidor de Power Pivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configuración inicial (PowerPivot para SharePoint)](http://msdn.microsoft.com/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)   
 [Instalación de PowerPivot para SharePoint 2010](http://msdn.microsoft.com/8d47dde7-c941-4280-a934-e2fe3f9a938f)  
  
  
