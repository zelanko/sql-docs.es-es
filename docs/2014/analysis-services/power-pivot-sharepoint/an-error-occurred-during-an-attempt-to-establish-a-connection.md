---
title: 'Error al intentar establecer una conexión con el origen de datos externo. No se pudieron actualizar las siguientes conexiones: datos de PowerPivot | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 36c9846ec1af5589f7fb29d3486ef11632eb01fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104567"
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
  
## <a name="see-also"></a>Vea también  
 [La conexión de datos utiliza la autenticación de Windows y las credenciales del usuario no se pudieron delegar No se pudieron actualizar las siguientes conexiones: datos de PowerPivot](the-data-connection-user-could-not-be-delegated.md)  
  
  