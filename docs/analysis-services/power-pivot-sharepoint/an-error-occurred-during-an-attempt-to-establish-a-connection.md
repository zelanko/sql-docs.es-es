---
title: Se produjo un error al intentar establecer una conexión | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ba4adc695a73cb3d12e98a3c27386f6656c0ff2e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection"></a>Se produjo un error al intentar establecer una conexión
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este error se produce si consulta datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un servidor que no tiene instalado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. También se produce si se detiene el servicio de SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) o si se intentan ver datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] desde una versión anterior.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Error en la conexión de datos.|  
|Texto del mensaje|Error al intentar establecer una conexión con el origen de datos externo. No se pudieron actualizar las siguientes conexiones: datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
  
## <a name="explanation"></a>Explicación  
 Excel Services devuelve este error en las siguientes situaciones: al consultar datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un libro de Excel que está publicado en SharePoint, si el entorno de SharePoint no tiene [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint Server o si se detiene el servicio SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]).  
  
 El error se produce al dividir o filtrar los datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cuando el motor de consulta no está disponible.  
  
## <a name="user-action"></a>Acción del usuario  
 Instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o mover el libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a un entorno de SharePoint que tiene instalado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Para obtener más información, consulte [Instalación de PowerPivot para SharePoint 2010](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f).  
  
 Si el software está instalado, compruebe que la instancia de SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) se esté ejecutando. Active **Administrar servicios en el servidor** en Administración Central. Seleccione también la aplicación de consola Servicios en Herramientas administrativas.  
  
 Para los libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se crearon en una versión de SQL Server 2008 R2 de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel, se debe instalar la versión SQL Server 2008 R2 del proveedor OLE DB de Analysis Services. Este error se producirá si ha instalado el proveedor, pero no registró el archivo Microsoft.AnalysisServices.ChannelTransport.dll. Para más información sobre el registro de archivo, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="see-also"></a>Vea también  
 [La conexión de datos utiliza la autenticación de Windows y no se pudieron delegar las credenciales de usuario. No se pudieron actualizar las siguientes conexiones: datos PowerPivot](../../analysis-services/power-pivot-sharepoint/the-data-connection-user-could-not-be-delegated.md)  
  
  
