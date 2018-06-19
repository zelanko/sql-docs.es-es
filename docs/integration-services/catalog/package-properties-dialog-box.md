---
title: Cuadro de diálogo de las propiedades de paquete | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageprop.general.f1
- sql13.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 47fac0923182e5c081f5c7ec76f3e51d17fff5b8
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35411277"
---
# <a name="package-properties-dialog-box"></a>Propiedades del paquete, cuadro de diálogo
  Utilice el cuadro de diálogo **Propiedades del paquete** para ver las propiedades de los paquetes almacenados en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para obtener más información, vea [Paquetes de Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md).  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo Propiedades del paquete](#open_dialog)  
  
-   [Configurar las opciones](#options)  
  
##  <a name="open_dialog"></a> Abrir el cuadro de diálogo Propiedades del paquete  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Se conectará a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos SSISDB.  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **SSISDB** .  
  
4.  Expanda la carpeta que contiene el paquete para el que desea ver las propiedades.  
  
5.  Haga clic con el botón derecho en el paquete y, después, seleccione **Propiedades**.  
  
##  <a name="options"></a> Configurar las opciones  
 Utilice la página **General** para ver las propiedades del paquete seleccionado.  
  
 Todas las propiedades que aparecen en la página **General** son de solo lectura.  
  
 **Nombre**  
 Muestra el nombre del paquete.  
  
 **Identificador**  
 Muestra el identificador del paquete.  
  
 **Punto de entrada**  
 El valor de **True** indica que el paquete se inicia directamente. El valor de **False** indica que el paquete debe iniciarse mediante otro paquete con la tarea Ejecutar paquete. El valor predeterminado es **True**.  
  
 Puede establecer esta propiedad en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] tanto para el paquete primario como para los paquetes secundarios. Para ello, haga clic con el botón derecho en el paquete en el Explorador de soluciones y, después, haga clic en **Paquete de punto de entrada**.  
  
 **Descripción**  
 Muestra la descripción opcional del paquete.  
  
  
