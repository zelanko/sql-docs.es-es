---
title: Cuadro de diálogo Validar | Microsoft Docs
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
- sql12.ssis.ssms.ispackagevalidate.f1
- sql12.ssis.ssms.isprojectvalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4b426080f2c76e8abc4bcaff26d2d5f0d53bfcc0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201202"
---
# <a name="validate-dialog-box"></a>Validar, cuadro de diálogo
  Use el cuadro de diálogo **Validar** para comprobar si hay problemas comunes en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un proyecto o paquete.  
  
 Si hay un problema, aparecerá un mensaje en la parte superior del cuadro de diálogo. De lo contrario, aparecerá el término Preparado en la parte superior.  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo Validar](#open_dialog)  
  
-   [Establecer las opciones de la página General](#general)  
  
##  <a name="open_dialog"></a> Abrir el cuadro de diálogo Validar  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Se conectará a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos SSISDB.  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **SSISDB** .  
  
4.  Expanda la carpeta que contiene el proyecto o paquete que desee validar.  
  
5.  Haga clic con el botón derecho en el paquete o proyecto y, después, haga clic en **Validar**.  
  
##  <a name="general"></a> Establecer las opciones de la página General  
 **Entorno**  
 Seleccione el entorno que desea usar para validar el proyecto o el paquete.  
  
 **Tiempo de ejecución de 32 bits**  
 Seleccione esta opción para usar un motor en tiempo de ejecución de 32 bits para ejecutar un paquete.  
  
 La pestaña **Parámetros** enumera los valores de parámetro que usa para validar el proyecto o el paquete. A continuación se exponen las opciones de la pestaña Parámetros.  
  
 **Contenedor**  
 Muestra el objeto que contiene el parámetro.  
  
 **Parámetro**  
 Muestra el nombre de los parámetros.  
  
 **Value**  
 Muestra el valor del parámetro.  
  
 La pestaña **Administradores de conexiones** enumera los valores de propiedad del administrador de conexión que usa para validar el proyecto o el paquete.  
  
 A continuación se exponen las opciones de la pestaña **Administradores de conexiones** .  
  
 **Contenedor**  
 Muestra el objeto que contiene el administrador de conexiones.  
  
 **Nombre**  
 Muestra el nombre del administrador de conexiones.  
  
 **Nombre de la propiedad**  
 Muestra el nombre de la propiedad del administrador de conexiones.  
  
 **Value**  
 Muestra el valor asignado a la propiedad del administrador de conexiones.  
  
  