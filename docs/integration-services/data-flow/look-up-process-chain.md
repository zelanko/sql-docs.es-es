---
title: Buscar cadena de procesos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6303ea4-fbbf-4cba-bc60-828df62be8c2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29791eaade29aa28089dfb579206c2dbddbed1ad
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="look-up-process-chain"></a>Buscar cadena de procesos
  Use el cuadro de diálogo **Buscar cadena de procesos** para buscar una cadena de procesos que se haya definido en el sistema de SAP Netweaver BW. Cuando aparezca la lista de las cadenas de procesos, seleccione la cadena que desee y el origen rellenará las opciones asociadas a los valores necesarios.  
  
 El origen de SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW usa el cuadro de diálogo **Buscar cadena de procesos** . Para obtener más información acerca del origen de SAP BW, vea [SAP BW Source](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir el cuadro de diálogo Buscar cadena de procesos**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el origen de SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de SAP BW.  
  
3.  En **Editor de origen de SAP BW**, haga clic en **Administrador de conexiones** para abrir la página **Administrador de conexiones** del editor.  
  
4.  En el cuadro del grupo **Cadena de procesos** , haga clic en **Buscar** para mostrar el cuadro de diálogo **Buscar cadena de procesos** .  
  
     El cuadro de grupo **Cadena de procesos** aparece solo si el valor de **Modo de ejecución** es **P -Desencadenar cadena de procesos**.  
  
## <a name="lookup-options"></a>Opciones de búsqueda  
 En los campos de búsqueda, puede filtrar los resultados mediante el carácter comodín de asterisco (*) o mediante una cadena parcial en combinación con el carácter comodín de asterisco. Sin embargo, si deja un campo de búsqueda vacío, la operación de búsqueda solamente se corresponderá con cadenas vacías en ese campo.  
  
 **Process chain**  
 Escriba el nombre de la cadena de procesos que desea buscar o un nombre parcial con el carácter comodín de asterisco (*). O bien, use el carácter comodín de asterisco por sí solo para incluir todas las cadenas de procesos.  
  
 **Buscar**  
 Permite buscar cadenas de procesos coincidentes que se hayan definido en el sistema SAP Netweaver BW.  
  
## <a name="lookup-results"></a>Buscar resultados  
 Después de hacer clic en el botón Buscar, aparece una lista de cadenas de procesos del sistema SAP Netweaver BW en una tabla con los siguientes encabezados de columna:  
  
 **Cadena de procesos**  
 Permite mostrar el nombre de la cadena de procesos que se haya definido en el sistema de SAP Netweaver BW.  
  
 **Descripción**  
 Permite mostrar la descripción de la cadena de procesos.  
  
 Cuando aparezca la lista de las cadenas de procesos, seleccione la cadena que desee y el origen rellenará las opciones asociadas a los valores necesarios.  
  
## <a name="see-also"></a>Ver también  
 [Editor de origen de SAP BW &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Ayuda F1 de Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
