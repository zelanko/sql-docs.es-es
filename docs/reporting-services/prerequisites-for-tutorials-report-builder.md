---
title: Requisitos previos para los tutoriales (Generador de informes) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
caps.latest.revision: "11"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: bc2107402e15e67c68815580a11d4f427db310c0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="prerequisites-for-tutorials-report-builder"></a>Requisitos previos para los tutoriales (Generador de informes)

Para realizar los tutoriales del Generador de informes, tiene que poder ver y guardar los informes paginados de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] en un servidor de informes o un sitio de SharePoint que esté integrado con un servidor de informes. Por lo que se refiere a los datos, todos los tutoriales usan consultas literales que deben ser procesadas por una instancia de SQL Server.  
  
Si no tiene acceso a un servidor de informes, un sitio o un origen de datos de informes, puede obtener información acerca del Generador de informes generando un informe sin conexión. Vea [Tutorial: Crear un informe de gráfico rápido sin conexión &#40;Generador de informes&#41;](../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  

## <a name="requirements"></a>Requisitos

Debe disponer de los siguientes requisitos previos para poder completar los tutoriales relativos al generador de informes:  
  
-   Acceso al Generador de informes. Puede ejecutar el Generador de informes de un servidor de informes de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o un servidor de informes de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] en modo integrado de SharePoint. El primer paso, cómo abrir el Generador de informes, es el único diferente en los diferentes servidores.  
  
    En un servidor de informes, seleccione **Nuevo** > **Informe paginado**.
  
    En un servidor de informes en el modo integrado de SharePoint, en la pestaña **Documentos** , seleccione **Nuevo documento**y, en la lista desplegable, seleccione **Informe del Generador de informes**. Por ejemplo, `http://<servername>/sites/mySite/reports`. El administrador de SharePoint debe habilitar la característica Informe del Generador de informes para cada biblioteca de documentos.  
  
-   La dirección URL a un servidor de informes de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o a un sitio de SharePoint integrado con un servidor de informes de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . Debe tener el permiso para guardar y ver informes, orígenes de datos compartidos, conjuntos de datos compartidos, elementos de informe y modelos. De manera predeterminada, la dirección URL de un servidor de informes es `http://<servername>/reportserver`. De manera predeterminada, la dirección URL de un sitio de SharePoint es `http://<sitename>` o `http://<server>/site`.  
  
-   El nombre de una instancia de SQL Server y las credenciales suficientes para el acceso de solo lectura a cualquier base de datos. Las consultas del conjunto de datos de los tutoriales usan datos literales, pero cada consulta debe ser procesada por una instancia de SQL Server para que devuelva los metadatos necesarios para un conjunto de datos de informe. Por ejemplo, la siguiente cadena de conexión especifica solo un servidor: `data source=<servername>`. Debe tener acceso de lectura a la base de datos predeterminada que le ha asignado el administrador del sistema que otorga los permisos de acceso al servidor. También puede especificar una base de datos, como se muestra en la siguiente cadena de conexión: `data source=<servername>;initial catalog=<database>`.  
  
-   Para el [Tutorial: Informe de asignaciones (Generador de informes)](Tutorial:%20Map%20Report%20\(Report%20Builder\).md), debe configurarse el servidor de informes para que admita mapas de Bing como fondo. Para obtener más información, consulte [Planear la compatibilidad de informe de mapa](http://msdn.microsoft.com/en-us/5ddc97a7-7ee5-475d-bc49-3b814dce7e19).   

-   El [Tutorial: Crear informes principales y de obtención de detalles (Generador de informes)](Tutorial:%20Creating%20Drillthrough%20and%20Main%20Reports%20\(Report%20Builder\).md) necesita acceso al cubo Contoso Sales. Para obtener más información, consulte el tutorial. 
  
El administrador del servidor de informes debe otorgarle los permisos necesarios en el servidor de informes, configurar las ubicaciones de carpeta de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] y configurar las opciones predeterminadas del Generador de informes. Para obtener más información, consulte [Instalar y desinstalar el Generador de informes](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416).  

## <a name="next-steps"></a>Pasos siguientes

[Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
