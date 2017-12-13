---
title: "Conectar la aplicación de servicio de Power Pivot para la aplicación Web de SharePoint en la entidad emisora de certificados | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7eacb900494941994ff38fd01f8b58e8939c1ebf
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="connect-power-pivot-service-app-to-sharepoint-web-app-in-ca"></a>Conectar la aplicación de servicio de Power Pivot para la aplicación Web de SharePoint en la entidad emisora de certificados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Un [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aplicación de servicio se puede utilizar cualquier número de aplicaciones Web de SharePoint en la granja de servidores. Para hacer que una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] esté disponible, agréguela a una lista de asociaciones de servicio.  
  
> [!IMPORTANT]  
>  Debe haber una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el grupo predeterminado para asegurarse de que el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] funciona correctamente. No agregue más de una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] al grupo predeterminado. Agregar varias entradas del mismo tipo de aplicación de servicio no se admite y podría producir errores. Si va a crear aplicaciones de servicio adicionales, agréguelas a listas personalizadas.  
  
 Este tema contiene las siguientes secciones:  
  
 [Agregar la aplicación de servicios PowerPivot al grupo predeterminado](#default)  
  
 [Agregar la aplicación de servicios PowerPivot a una lista de asociaciones de servicio personalizada](#custom)  
  
##  <a name="default"></a> Agregar la aplicación de servicios al grupo predeterminado  
 Una lista de asociaciones de servicio es una lista de servicios compartidos que proporcionan recursos a otras aplicaciones web de SharePoint en la granja. Hay un grupo predeterminado de asociaciones del servicio para la granja.  
  
 Para estar en la lista, una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] puede agregarse al crear la aplicación o después siguiendo estos pasos.  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Configurar las asociaciones de aplicación de servicio**.  
  
2.  En Grupo de proxy de aplicación, haga clic en **predeterminado**.  
  
3.  Active la casilla situada al lado de la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (indicada por el nombre de tipo **Proxy de la aplicación de servicio PowerPivot**). Si tiene más de una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , simplemente elija una.  
  
4.  Haga clic en **Aceptar**.  
  
##  <a name="custom"></a> Agregar la aplicación de servicios [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a una lista de asociaciones de servicio personalizada  
 El grupo personalizado puede reemplazar a una lista predeterminada. Una lista personalizada se crea específicamente para una sola aplicación web de SharePoint. Invalida el grupo predeterminado y lo reemplaza solo con las asociaciones de servicio que un administrador o servicio de la granja especifique. Si creó varias aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , debe utilizar una lista personalizada para especificar cuál utilizar. Otras aplicaciones web no pueden reutilizar una lista personalizada. Solo se aplica a la aplicación web para la que se creó.  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Administrar aplicaciones web**.  
  
2.  Seleccione la aplicación (por ejemplo, SharePoint -80).  
  
3.  En Aplicaciones web, en Administrar, haga clic en **Conexiones de servicio**.  
  
4.  En **Editar el siguiente grupo de conexiones**, seleccione **[personalizado]**.  
  
5.  Active la casilla situada al lado de cada conexión de aplicación de servicio que desee utilizar. Si tiene varias aplicaciones de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (indicadas por el tipo establecido en **Proxy de la aplicación de servicio PowerPivot**), elija solo una.  
  
6.  Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Creación y configuración de una aplicación de servicio PowerPivot en Administración central](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Configuración inicial (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)  
  
  
