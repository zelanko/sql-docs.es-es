---
title: 'Error al intentar establecer una conexión con el origen de datos externo. No se pudieron actualizar las siguientes conexiones: datos PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 242fefb2ca22d7b0129268a8a3ea8ed98e80bbe3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547617"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection-to-the-external-data-source-the-following-connections-failed-to-refresh-powerpivot-data"></a>Error al intentar establecer una conexión con el origen de datos externo. No se pudieron actualizar las siguientes conexiones: datos PowerPivot
  Este error se produce si consulta los datos PowerPivot en un servidor que no tiene instalado PowerPivot para SharePoint. También se produce si se detiene el servicio SQL Server Analysis Services (PowerPivot) o si se intenta ver los datos PowerPivot de una versión anterior.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|PowerPivot para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Error en la conexión de datos.|  
|Texto del mensaje|Error al intentar establecer una conexión con el origen de datos externo. No se pudieron actualizar las siguientes conexiones: datos PowerPivot|  
  
## <a name="explanation"></a>Explicación  
 Excel Services devuelve este error al consultar los datos PowerPivot en un libro de Excel que está publicado en SharePoint si el entorno de SharePoint no tiene un servidor PowerPivot para SharePoint o si se detiene la instancia del servicio SQL Server Analysis Services (PowerPivot).  
  
 El error se produce al dividir o filtrar los datos PowerPivot cuando el motor de consulta no está disponible.  
  
## <a name="user-action"></a>Acción del usuario  
 Instale PowerPivot para SharePoint o mueva el libro PowerPivot a un entorno de SharePoint que tenga instalado PowerPivot para SharePoint. Para obtener más información, vea [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 Si el software está instalado, compruebe que la instancia de SQL Server Analysis Services (PowerPivot) se esté ejecutando. Active **Administrar servicios en el servidor** en Administración Central. Seleccione también la aplicación de consola Servicios en Herramientas administrativas.  
  
 Para los libros PowerPivot que se crearon en una versión SQL Server 2008 R2 de PowerPivot para Excel, se debe instalar la versión SQL Server 2008 R2 del proveedor OLE DB de Analysis Services. Este error se producirá si ha instalado el proveedor, pero no registró el archivo Microsoft.AnalysisServices.ChannelTransport.dll. Para más información sobre el registro de archivo, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
## <a name="see-also"></a>Consulte también  
 [La conexión de datos utiliza la autenticación de Windows y las credenciales de usuario no se pudieron delegar. No se pudieron actualizar las siguientes conexiones: datos PowerPivot](the-data-connection-user-could-not-be-delegated.md)  
  
  
