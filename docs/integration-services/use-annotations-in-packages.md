---
description: Usar anotaciones en paquetes
title: Usar anotaciones en paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- self-documenting packages
- adding annotations
- annotations [Integration Services]
ms.assetid: 48c8ed9a-b10d-490c-9ba7-4b77aa44e3dd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 88a927a23696e5de7a1e079cb517078dc318b69c
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "92193767"
---
# <a name="use-annotations-in-packages"></a>Usar anotaciones en paquetes

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  El Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] proporciona anotaciones, que puede usar para que los paquetes se autodocumenten y sean más fáciles de entender y mantener. Puede agregar anotaciones a las superficies de diseño de flujo de control, flujo de datos y controlador de eventos del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] . Las anotaciones pueden contener cualquier tipo de texto y resultan útiles para agregar etiquetas, comentarios y demás información descriptiva a un paquete. Las anotaciones únicamente son una característica de tiempo de diseño. Por ejemplo, no se escriben en los registros.  
  
 Cuando se presiona ENTRAR, el texto se ajusta a la línea siguiente. El cuadro de anotación aumenta de tamaño automáticamente a medida que agrega líneas de texto adicionales. Las anotaciones de paquetes se guardan como texto sin cifrar en la sección CDATA del archivo de paquete.  
  
 Para obtener más información sobre los cambios en el formato del archivo de paquete, vea [Formato de paquetes SSIS](./integration-services-ssis-packages.md).  
  
 Cuando se guarda un paquete, el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] guarda las anotaciones en el paquete.  
  
## <a name="add-an-annotation-to-a-package"></a>agregar una anotación a un paquete  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete al que desea agregar una anotación.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic con el botón derecho en cualquier parte de la superficie de diseño de la pestaña **Flujo de control**, **Flujo de datos** o **Controlador de eventos** y, luego, haga clic en **Agregar anotación**. Aparece un bloque de texto en la superficie de diseño de la pestaña.  
  
4.  Agregue el texto.  
  
    > [!NOTE]  
    >  Si no agrega texto, el bloque de texto se elimina al hacer clic fuera del bloque.  
  
5.  Para cambiar el tamaño o el formato del texto de la anotación, haga clic con el botón derecho en la anotación y, después, haga clic en **Establecer fuente para anotaciones de texto**.  
  
6.  Para agregar una línea de texto adicional, presione ENTRAR.  
  
     El cuadro de anotación aumenta de tamaño automáticamente a medida que agrega líneas de texto adicionales.  
  
7.  Para agregar una anotación a un grupo, haga clic con el botón derecho en la anotación y haga clic en **Grupo**.  
  
8.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar todo**.