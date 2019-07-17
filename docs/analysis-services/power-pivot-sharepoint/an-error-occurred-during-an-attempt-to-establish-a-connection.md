---
title: Se produjo un error durante un intento para establecer una conexión | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28d5bd077da96e3dd6f8a48004c3a5df1b681f61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208354"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection"></a>Se produjo un error durante un intento para establecer una conexión
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este error se produce si consulta datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un servidor que no tiene instalado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. También se produce si el equipo con SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) se detiene el servicio, o si está intentando ver [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] datos desde una versión anterior.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Error en la conexión de datos.|  
|Texto del mensaje|Error al intentar establecer una conexión con el origen de datos externo. No se pudieron actualizar las siguientes conexiones: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Datos|  
  
## <a name="explanation"></a>Explicación  
 Excel Services devuelve este error al consultar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] datos en un libro de Excel que esté publicado en SharePoint y el entorno de SharePoint no tienen un [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint server o SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) se ha detenido el servicio.  
  
 El error se produce al dividir o filtrar los datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cuando el motor de consulta no está disponible.  
  
## <a name="user-action"></a>Acción del usuario  
 Instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o mover el libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a un entorno de SharePoint que tiene instalado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Para obtener más información, consulte [Instalación de PowerPivot para SharePoint 2010](http://msdn.microsoft.com/8d47dde7-c941-4280-a934-e2fe3f9a938f).  
  
 Si está instalado el software, compruebe que el SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) se está ejecutando la instancia. Active **Administrar servicios en el servidor** en Administración Central. Seleccione también la aplicación de consola Servicios en Herramientas administrativas.  
  
 Para los libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se crearon en una versión de SQL Server 2008 R2 de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel, se debe instalar la versión SQL Server 2008 R2 del proveedor OLE DB de Analysis Services. Este error se producirá si ha instalado el proveedor, pero no registró el archivo Microsoft.AnalysisServices.ChannelTransport.dll. Para más información sobre el registro de archivo, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="see-also"></a>Vea también  
 [La conexión de datos utiliza la autenticación de Windows y las credenciales del usuario no se pudieron delegar No se pudieron actualizar las siguientes conexiones: Datos de Power Pivot](../../analysis-services/power-pivot-sharepoint/the-data-connection-user-could-not-be-delegated.md)  
  
  
