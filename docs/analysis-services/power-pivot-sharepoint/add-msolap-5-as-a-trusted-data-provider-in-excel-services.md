---
title: Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d7576aadda3739709acdffcb1b2419c20d39ed4e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164456"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  MSOLAP.5 hace referencia al proveedor OLE DB de Analysis Services para SQL Server 2012. Excel Services debe confiar en este proveedor para que pueda realizar la solicitud de conexión que tiene como resultado la disponibilidad de los datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un servidor.  
  
 Si configuró [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint mediante la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , MSOLAP.5 ya puede ser proveedor de confianza porque la herramienta incluye una acción que cumple este requisito. Sin embargo, si usa PowerShell, Administración central, o si se excluyó la acción de proveedor de confianza en la herramienta de configuración, es posible que no se encuentre el proveedor. En ese caso, debe agregarlo como parte de la configuración de la granja de servidores para el acceso a datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Solo necesita realizar este paso una vez para cada aplicación de servicios de Excel Services.  
  
 Cada servidor físico que controla una solicitud de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , como un servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o un servidor de Excel Services, debe tener instalado el proveedor OLE DB en el equipo. Una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint incluye siempre el proveedor OLE DB, pero si Excel Services se ejecuta en un equipo que no dispone de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, debe instalar el proveedor manualmente. Para más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Agregue un proveedor de confianza en Excel Services  
  
1.  En Administración central, haga clic en **Administrar aplicaciones de servicio**y haga clic en la aplicación de servicios de Excel Services.  
  
2.  Haga clic en **Proveedores de datos de confianza**.  
  
3.  Compruebe que MSOLAP.5 aparece en la lista. Según el modo en que configuró [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, MSOLAP.5 podría ya ser de confianza.  
  
4.  Si no aparece, haga clic en **Agregar proveedor de datos de confianza**.  
  
5.  En el identificador del proveedor, escriba **MSOLAP.5**.  
  
6.  En Tipo de proveedor, asegúrese de que está seleccionado OLE DB.  
  
7.  En Descripción del proveedor, escriba **Proveedor OLE DB de Microsoft para OLAP Services 11.0**.  
  
  
