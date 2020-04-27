---
title: Cuadro de diálogo Examinar todas las entidades de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 46d6fd5d4ecd821a3ccfeb35679e8fa7bab6104e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771725"
---
# <a name="browse-all-principals-dialog-box"></a>Examinar todas las entidades (cuadro de diálogo)
  Use el cuadro de diálogo **Examinar todas las entidades** para seleccionar la entidad de seguridad de base de datos a la que desea cambiar los permisos en el proyecto seleccionado o en todos los proyectos incluidos en una carpeta seleccionada.  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo Examinar todas las entidades](#open_dialog)  
  
-   [Configurar las opciones](#options)  
  
##  <a name="open-the-browse-all-principals-dialog-box"></a><a name="open_dialog"></a> Abrir el cuadro de diálogo Examinar todas las entidades  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Se conectará a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda el catálogo SSISDB.  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **SSISDB** .  
  
4.  Para cambiar los permisos de la entidad de seguridad en todos los proyectos incluidos en una carpeta seleccionada, haga clic con el botón derecho en la carpeta y después haga clic en **Propiedades**.  
  
     Para cambiar los permisos de la entidad de seguridad en un proyecto seleccionado, expanda la carpeta que contiene el proyecto, haga clic con el botón derecho en él y después haga clic en **Propiedades**.  
  
5.  Seleccione la página **Permisos** y haga clic en **Examinar**.  
  
##  <a name="configure-the-options"></a><a name="options"></a> Configurar las opciones  
 En esta página se muestran las entidades de seguridad de la vista de catálogo, sys.database_principals, de la base de datos de SSISDB.  
  
 Si selecciona las entidades de seguridad, se agregarán a la lista **Inicios de sesión o roles** de la página **Permisos** del cuadro de diálogo principal cuando haga clic en **Aceptar** y cierre el cuadro de diálogo **Examinar todas las entidades** . Después de agregar entidades de seguridad a la lista de **Inicios de sesión o roles** , puede cambiar sus permisos en el proyecto seleccionado.  
  
 **Columna de selección**  
 Seleccione esta opción para agregar la entidad de seguridad a la lista **Inicios de sesión o roles** de la página **Permisos** del cuadro de diálogo principal.  
  
 **Columna de icono**  
 Icono que corresponde al **Tipo** de la entidad de seguridad.  
  
 **Nombre**  
 Nombre de la entidad de seguridad.  
  
 **Tipo**  
 Tipo de la entidad de seguridad. Los tipos comunes son:  
  
-   Usuario de SQL  
  
-   Usuario de Windows  
  
-   Rol de base de datos  
  
  
