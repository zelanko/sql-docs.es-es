---
title: Combinaciones admitidas de SQL Server Reporting Services y SharePoint | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 07/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 507c09d09f22f8326898b557997bc109785f30c0
ms.contentlocale: es-es
ms.lasthandoff: 07/03/2017

---

# Combinaciones admitidas de SharePoint y el servidor de Reporting Services
<a id="supported-combinations-of-sharepoint-and-reporting-services-server" class="xliff"></a>

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Un servidor de informes de SQL Server Reporting Services instalado en modo de SharePoint requiere una versión de SharePoint y el SQL Server Reporting Services complemento (rsSharePoint.msi) para productos de SharePoint, que se instalan en los servidores de SharePoint. En este tema se resumen las combinaciones admitidas.

> [!NOTE]
> Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

## Combinaciones admitidas de los componentes de Reporting Services y SharePoint
<a id="supported-combinations-of-sharepoint-and-reporting-services-components" class="xliff"></a>

 En la tabla siguiente se resumen las combinaciones admitidas de servidor de informes, complemento de Reporting Services para productos de SharePoint y productos de SharePoint. Las combinaciones que no se muestran en la tabla siguiente no se admiten

### Combinaciones admitidas
<a id="supported-combinations" class="xliff"></a>

||Servidor de informes|Complemento|Versión de SharePoint|
|-|-------------------|-------------|------------------------|
|1|SQL Server 2016|SQL Server 2016|SharePoint 2016|
|2|SQL Server 2016|SQL Server 2016|SharePoint 2013|
|3|SQL Server 2014|SQL Server 2014|SharePoint 2013|
|4|SQL Server 2014|SQL Server 2014|SharePoint 2010|
|5|SQL Server 2012 SP3|SQL Server 2014 y SQL Server 2012 SP3|SharePoint 2013|
|6|SQL Server 2012 SP2|SQL Server 2014 y SQL Server 2012 SP2|SharePoint 2013|
|7|SQL Server 2012 SP1|SQL Server 2014 y SQL Server 2012 SP1|SharePoint 2013|
|8|SQL Server 2012 y SQL Server 2012 SP1 *|SQL Server 2014|SharePoint 2010|
|9|SQL Server 2012|SQL Server 2012|SharePoint 2010|
|10|SQL Server 2008 R2|SQL Server 2014|SharePoint 2010|
|11|SQL Server 2008 R2|SQL Server 2012 y SQL Server 2012 SP1 o posterior|SharePoint 2010|
|12|SQL Server 2008 R2|SQL Server 2008 R2|SharePoint 2010|
|13|SQL Server 2008 R2|SQL Server 2008 SP2|SharePoint 2007|
|14|SQL Server 2008 SP2|SQL Server 2008 R2|SharePoint 2010|
|15|SQL Server 2008 SP2|SQL Server 2008 y SQL Server 2008 SP2|SharePoint 2007|

 *Excepción: no se admite la integración de Power View.

 Para obtener vínculos a las páginas de descarga del complemento, vea [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  

 **Notas adicionales:**

- Asegúrese de actualizar todos los servidores de SharePoint dentro de la granja de servidores. Esto incluye los servidores de front-end web y de aplicación.

- La compatibilidad con SharePoint 2016, incluida la integración de Power View, requiere el servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la versión del complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de SQL Server 2016 o posterior.

- La compatibilidad con SharePoint 2013, incluida la integración de Power View, requiere el servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la versión del complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de SQL Server 2012 SP1 o posterior.

- Power View se presentó en SQL Server 2012. Por lo tanto, la integración de Power View con SharePoint 2010 requiere que SQL Server 2012 o posterior del complemento.

- Los servidores de informes de SQL Server 2012 (o posterior) no admiten el complemento de SQL Server 2008 R2. El instalador de requisitos previos de SharePoint 2010 instala automáticamente el complemento de SQL Server 2008 R2. Debe desinstalarse antes de instalar las versiones más recientes del complemento. No se admite la actualización en contexto del complemento.

- **Actualización:** SharePoint 2010 con el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no se puede actualizar en contexto a SharePoint 2013. SharePoint 2013 requiere SQL Server 2012 SP1 o una versión posterior de la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] server complemento y el informe. Para obtener más información acerca de la actualización, vea [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).

## Pasos siguientes
<a id="next-steps" class="xliff"></a>

 [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
