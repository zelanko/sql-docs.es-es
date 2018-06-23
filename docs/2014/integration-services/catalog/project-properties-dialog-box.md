---
title: Cuadro de diálogo Propiedades del proyecto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.ssms.isprojectprop.general.f1
- sql12.ssis.ssms.isprojectprop.permissions.f1
ms.assetid: d5cf52f5-1fe2-438a-98a3-fe117360acf8
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 564ea56b167f5fd478daac07a36e655486704697
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203011"
---
# <a name="project-properties-dialog-box"></a>Propiedades del proyecto (cuadro de diálogo)
  Un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es una unidad de implementación. Cada proyecto puede contener paquetes, parámetros y referencias de entorno. Un proyecto es un objeto protegible y puede definir permisos en las entidades de seguridad de base de datos. Cuando se vuelve a implementar un proyecto, la versión anterior del mismo puede almacenarse en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Los parámetros del proyecto y los parámetros del paquete se pueden utilizar para asignar valores a las propiedades de los paquetes en el momento de la ejecución. Algunos parámetros requieren valores para que el paquete se pueda ejecutar. Los valores de parámetros que hacen referencia a las variables de entorno requieren que el proyecto tenga la referencia de entorno correspondiente antes de la ejecución.  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo de Propiedades del proyecto](#open_dialog)  
  
-   [Establecer las opciones de la página General](#general)  
  
-   [Establecer las opciones de la página Permisos](#permissions)  
  
##  <a name="open_dialog"></a> Abrir el cuadro de diálogo de Propiedades del proyecto  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Se conectará a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos SSISDB.  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **SSISDB** .  
  
4.  Expanda la carpeta que contiene el proyecto para el que desea establecer las propiedades.  
  
5.  Haga clic con el botón derecho en el proyecto y, después, haga clic en **Propiedades**.  
  
##  <a name="general"></a> Establecer las opciones de la página General  
 Use la página General para ver las propiedades del proyecto.  
  
 **Nombre**  
 Muestra el nombre del proyecto.  
  
 **Identificador**  
 Muestra el identificador del proyecto.  
  
 **Descripción**  
 Muestra la descripción opcional del proyecto.  
  
 **Versión del proyecto**  
 Muestra la versión del proyecto.  
  
 **Fecha de implementación**  
 Muestra la fecha y hora en que el proyecto se implementó por primera vez o se volvió a implementar.  
  
##  <a name="permissions"></a> Establecer las opciones de la página Permisos  
 Use la página **Permisos** para ver y establecer permisos explícitos para el proyecto.  
  
 Examinar  
 Haga clic en **Examinar** para seleccionar los usuarios y los roles para los que quiere establecer permisos con el cuadro de diálogo **Examinar todas las entidades** .  
  
 **Nombre**  
 Muestra el nombre del usuario o del rol.  
  
 **Tipo**  
 Muestra el tipo de usuario o de rol.  
  
 **Permiso**  
 Muestra los permisos.  
  
 **Otorgante de permisos**  
 Muestra el usuario o el rol que concede el permiso.  
  
 **Conceder**  
 Al seleccionar **Conceder** , se concede el permiso al usuario o al rol seleccionado.  
  
 **Denegar**  
 Al seleccionar **Denegar** , se deniega el permiso al usuario o al rol seleccionado.  
  
  