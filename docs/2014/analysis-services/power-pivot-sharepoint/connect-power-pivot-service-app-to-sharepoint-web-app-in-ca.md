---
title: Conectar una aplicación de servicio PowerPivot a una aplicación Web de SharePoint en Administración Central | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 33d2f83b1b003e6be2fc5c47b8a0e12b440f537c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749426"
---
# <a name="connect-a-powerpivot-service-application-to-a-sharepoint-web-application-in-central-administration"></a>Conectar una aplicación de servicio PowerPivot a una aplicación Web de SharePoint en Administración Central
  Una aplicación de servicio PowerPivot puede ser utilizada por cualquier número de aplicaciones web de SharePoint de la granja de servidores. Para hacer que una aplicación de servicio PowerPivot esté disponible, agréguela a una lista de asociaciones de servicio.  
  
> [!IMPORTANT]  
>  Debe haber una aplicación de servicio PowerPivot en el grupo predeterminado para asegurarse de que el Panel de administración de PowerPivot funciona correctamente. No agregue más de una aplicación de servicio PowerPivot al grupo predeterminado. Agregar varias entradas del mismo tipo de aplicación de servicio no se admite y podría producir errores. Si va a crear aplicaciones de servicio adicionales, agréguelas a listas personalizadas.  
  
 Este tema contiene las siguientes secciones:  
  
 [Agregar la aplicación de servicios PowerPivot al grupo predeterminado](#default)  
  
 [Agregar una lista de asociaciones de servicio personalizado de aplicación de servicios de PowerPivot](#custom)  
  
##  <a name="default"></a> Agregar la aplicación de servicios PowerPivot al grupo predeterminado  
 Una lista de asociaciones de servicio es una lista de servicios compartidos que proporcionan recursos a otras aplicaciones web de SharePoint en la granja. Hay un grupo predeterminado de asociaciones del servicio para la granja.  
  
 Para estar en la lista, una aplicación de servicio PowerPivot puede agregarse al crear la aplicación o después siguiendo estos pasos.  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Configurar las asociaciones de aplicación de servicio**.  
  
2.  En Grupo de proxy de aplicación, haga clic en **predeterminado**.  
  
3.  Active la casilla situada al lado de la aplicación de servicio PowerPivot (lo que se indica por el nombre de tipo `PowerPivot Service Application Proxy`). Si tiene más de una aplicación de servicio PowerPivot, simplemente elija una.  
  
4.  Haga clic en **Aceptar**.  
  
##  <a name="custom"></a> Agregar una lista de asociaciones de servicio personalizado de aplicación de servicios de PowerPivot  
 El grupo personalizado puede reemplazar a una lista predeterminada. Una lista personalizada se crea específicamente para una sola aplicación web de SharePoint. Invalida el grupo predeterminado y lo reemplaza solo con las asociaciones de servicio que un administrador o servicio de la granja especifique. Si creó varias aplicaciones de servicio PowerPivot, debe utilizar una lista personalizada para especificar cuál utilizar. Otras aplicaciones web no pueden reutilizar una lista personalizada. Solo se aplica a la aplicación web para la que se creó.  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Administrar aplicaciones web**.  
  
2.  Seleccione la aplicación (por ejemplo, SharePoint -80).  
  
3.  En Aplicaciones web, en Administrar, haga clic en **Conexiones de servicio**.  
  
4.  En **Editar el siguiente grupo de conexiones**, seleccione **[personalizado]**.  
  
5.  Active la casilla situada al lado de cada conexión de aplicación de servicio que desee utilizar. Si tiene varias aplicaciones de servicio PowerPivot (que se indican con el tipo establecido en `PowerPivot Service Application Proxy`), asegúrese de elegir solo una.  
  
6.  Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Crear y configurar una aplicación de servicio PowerPivot en Administración Central](create-and-configure-power-pivot-service-application-in-ca.md)   
 [Configuración inicial &#40;PowerPivot para SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)  
  
  
