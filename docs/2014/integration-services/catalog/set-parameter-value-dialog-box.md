---
title: Cuadro de diálogo Establecer valor de parámetro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ce9c2201-4e9a-4495-948f-b68deeaa7955
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f79c0ceeb0f1fba931ab4b781a677c85ccc99933
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202777"
---
# <a name="set-parameter-value-dialog-box"></a>Cuadro de diálogo Establecer valor de parámetro
  Utilice el cuadro de diálogo **Establecer valor de parámetro** para establecer los valores de los parámetros y las propiedades de administrador de conexiones, para los proyectos y los paquetes.  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo Establecer valor de parámetro](#open_dialog)  
  
-   [Configurar las opciones](#option)  
  
##  <a name="open_dialog"></a> Abrir el cuadro de diálogo Establecer valor de parámetro  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Se conectará a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos SSISDB.  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **SSISDB** .  
  
4.  Haga clic con el botón derecho en un paquete o proyecto, haga clic en **Configurar**y, luego, haga clic en el botón de puntos suspensivos de la pestaña **Parámetros** o en la pestaña **Administradores de conexiones** .  
  
##  <a name="option"></a> Configurar las opciones  
 **Parámetro**  
 Muestra el nombre de parámetro.  
  
 **Tipo**  
 Enumera el tipo de datos del valor de parámetro.  
  
 **Descripción**  
 Muestra una descripción opcional del parámetro.  
  
 **Editar valor**  
 Seleccione esta opción para editar el valor del parámetro.  
  
 **Usar valor predeterminado del paquete**  
 Seleccione esta opción para usar el valor predeterminado del parámetro almacenado en este paquete.  
  
 **Usar la variable de entorno**  
 Seleccione esta opción para usar un valor de variable almacenado en el entorno, al que hace referencia el proyecto o el paquete. Para agregar una referencia de entorno a un proyecto o a un paquete, use el cuadro de diálogo **Configurar** . Para más información, consulte [Configure Dialog Box](configure-dialog-box.md).  
  
  