---
title: Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 146b61a544dfc91585cde88bbdb54d2f43375b0f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]MSOLAP.5 hace referencia al proveedor OLE DB de Analysis Services para SQL Server 2012. Excel Services debe confiar en este proveedor para que pueda realizar la solicitud de conexión que tiene como resultado la disponibilidad de los datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un servidor.  
  
 Si configuró [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint mediante la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , MSOLAP.5 ya puede ser proveedor de confianza porque la herramienta incluye una acción que cumple este requisito. Sin embargo, si usa PowerShell, Administración central, o si se excluyó la acción de proveedor de confianza en la herramienta de configuración, es posible que no se encuentre el proveedor. En ese caso, debe agregarlo como parte de la configuración de la granja de servidores para el acceso a datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Solo necesita realizar este paso una vez para cada aplicación de servicios de Excel Services.  
  
 Cada servidor físico que controla una solicitud de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , como un servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o un servidor de Excel Services, debe tener instalado el proveedor OLE DB en el equipo. Una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint incluye siempre el proveedor OLE DB, pero si Excel Services se ejecuta en un equipo que no dispone de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, debe instalar el proveedor manualmente. Para más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Agregue un proveedor de confianza en Excel Services  
  
1.  En Administración central, haga clic en **Administrar aplicaciones de servicio**y haga clic en la aplicación de servicios de Excel Services.  
  
2.  Haga clic en **Proveedores de datos de confianza**.  
  
3.  Compruebe que MSOLAP.5 aparece en la lista. Según el modo en que configuró [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, MSOLAP.5 podría ya ser de confianza.  
  
4.  Si no aparece, haga clic en **Agregar proveedor de datos de confianza**.  
  
5.  En el identificador del proveedor, escriba **MSOLAP.5**.  
  
6.  En Tipo de proveedor, asegúrese de que está seleccionado OLE DB.  
  
7.  En Descripción del proveedor, escriba **Proveedor OLE DB de Microsoft para OLAP Services 11.0**.  
  
  
