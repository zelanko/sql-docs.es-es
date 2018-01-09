---
title: "Activar la integración de Power Pivot para colecciones de sitios en la entidad emisora de certificados | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 52fb43ddd40e432cb174c9d0794a3919fc48ff7a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="activate-power-pivot-integration-for-site-collections-in-ca"></a>Activar la integración de Power Pivot para colecciones de sitios en la entidad emisora de certificados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Activar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] integración de características para colecciones de sitios concretos es necesaria si utiliza la opción de instalación de granja de servidores existente para instalar SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Si ha instalado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint con la opción Nuevo servidor, puede omitir esta tarea, porque el programa de instalación de SQL Server ya ha activado la integración de características de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para la colección de sitios raíz al configurar la implementación.  
  
 Es necesario activar las características en el nivel de colección de sitios para que las plantillas y las páginas de las aplicaciones estén disponibles para los sitios, incluidas las páginas de configuración para la actualización de datos programada y las páginas de aplicación para las bibliotecas de Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y de fuentes de distribución de datos.  
  
 Debe activar la integración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para cada colección de sitios que admita el procesamiento de consultas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## <a name="prerequisites"></a>Prerequisites  
 Debe ser administrador de la colección de sitios.  
  
## <a name="activate-power-pivot-features"></a>Activar las características de PowerPivot  
  
1.  En un sitio de SharePoint, haga clic en **Acciones de sitio**.  
  
     De forma predeterminada, se tiene acceso a las aplicaciones web de SharePoint a través del puerto 80. Esto significa que puede acceder a menudo un sitio de SharePoint escribiendo http://\<nombre de equipo > para abrir la colección de sitios raíz.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  En Administración de la colección de sitios, haga clic en **Características de la colección de sitios**.  
  
4.  Desplácese hacia abajo en la página hasta que encuentre **Característica de colección de sitios de integración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
5.  Haga clic en **Activar**.  
  
6.  Repita este procedimiento con las demás colecciones de sitios abriendo cada sitio y haciendo clic en **Acciones de sitio**.  
  
## <a name="see-also"></a>Ver también  
 [Administración y configuración del servidor de Power Pivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configuración inicial (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)   
 [Instalación de PowerPivot para SharePoint 2010](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)  
  
  
