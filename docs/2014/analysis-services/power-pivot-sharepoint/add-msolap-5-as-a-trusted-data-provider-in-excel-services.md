---
title: Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 354ca92c8ed66c7669863cc234fe4999ab95e662
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051190"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services
  MSOLAP.5 hace referencia al proveedor OLE DB de Analysis Services para SQL Server 2012. Excel Services debe confiar en este proveedor para que pueda realizar la solicitud de conexión que tiene como resultado la disponibilidad de los datos de PowerPivot en un servidor.  
  
 Si configuró PowerPivot para SharePoint mediante la herramienta de configuración de PowerPivot, MSOLAP.5 ya puede ser proveedor de confianza porque la herramienta incluye una acción que cumple este requisito. Sin embargo, si usa PowerShell o, si se excluyó la acción de proveedor de confianza en la herramienta de configuración, es posible que no se encuentre Administración central o el proveedor. En ese caso, debe agregarlos como parte de la configuración de la granja de servidores para el acceso a datos PowerPivot.  
  
 Solo necesita realizar este paso una vez para cada aplicación de servicios de Excel Services.  
  
 Cada servidor físico que controla una solicitud de datos PowerPivot, como un servidor PowerPivot para SharePoint o un servidor de Excel Services, debe tener instalado el proveedor OLE DB en el equipo. Una instalación de PowerPivot para SharePoint incluye siempre el proveedor OLE DB, pero si Excel Services se ejecuta en un equipo que no dispone de PowerPivot para SharePoint, debe instalar el proveedor manualmente. Para obtener más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Agregue un proveedor de confianza en Excel Services  
  
1.  En Administración central, haga clic en **Administrar aplicaciones de servicio**y haga clic en la aplicación de servicios de Excel Services.  
  
2.  Haga clic en **Proveedores de datos de confianza**.  
  
3.  Compruebe que MSOLAP.5 aparece en la lista. Según el modo en que configuró PowerPivot para SharePoint, MSOLAP.5 podría ya ser de confianza.  
  
4.  Si no aparece, haga clic en **Agregar proveedor de datos de confianza**.  
  
5.  Identificador de proveedor, escriba `MSOLAP.5`.  
  
6.  En Tipo de proveedor, asegúrese de que está seleccionado OLE DB.  
  
7.  En Descripción del proveedor, escriba **Proveedor OLE DB de Microsoft para OLAP Services 11.0**.  
  
  
