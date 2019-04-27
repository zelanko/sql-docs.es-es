---
title: Cuadro de diálogo Validar | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectvalidate.f1
- sql13.ssis.ssms.ispackagevalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8380b3ff1502088e0131b182149e90e31d2be42c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771658"
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
  
 **Valor**  
 Muestra el valor del parámetro.  
  
 La pestaña **Administradores de conexiones** enumera los valores de propiedad del administrador de conexión que usa para validar el proyecto o el paquete.  
  
 A continuación se exponen las opciones de la pestaña **Administradores de conexiones** .  
  
 **Contenedor**  
 Muestra el objeto que contiene el administrador de conexiones.  
  
 **Name**  
 Muestra el nombre del administrador de conexiones.  
  
 **Nombre de la propiedad**  
 Muestra el nombre de la propiedad del administrador de conexiones.  
  
 **Valor**  
 Muestra el valor asignado a la propiedad del administrador de conexiones.  
  
  
