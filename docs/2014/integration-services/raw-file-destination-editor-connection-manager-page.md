---
title: Editor de destino de archivos sin formato (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledestinationconnectionmanager.f1
ms.assetid: a0ec9643-3b44-4467-b855-f45ae4794f7f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2677d0dd1f4697177171ba0edd4641ec02110310
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056564"
---
# <a name="raw-file-destination-editor-connection-manager-page"></a>Editor de destino de archivos sin formato (página Administrador de conexiones)
  Use el editor de destino de archivos sin formato para configurar el destino de archivo sin formato con el fin de escribir datos sin formato en un archivo.  
  
 **¿Qué desea hacer?**  
  
-   [Abra el editor de destino de archivos sin formato](#open)  
  
-   [Establecer opciones en la pestaña Administrador de conexiones](#connection)  
  
-   [Establecer las opciones de la pestaña Columnas](#mapping)  
  
##  <a name="open"></a> Abra el editor de destino de archivos sin formato  
  
1.  Agregue el destino de archivo sin formato a un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el componente y, después, haga clic en **Editar**.  
  
##  <a name="connection"></a> Establecer opciones en la pestaña Administrador de conexiones  
 **Modo de acceso**  
 Seleccione cómo se especifica el nombre de archivo. Seleccione **Nombre de archivo** para escribir el nombre de archivo y la ruta de acceso directamente o **Nombre de archivo de la variable** para especificar una variable que contiene el nombre de archivo.  
  
 **Nombre de archivo** o **Nombre de variable**  
 Escriba el nombre y la ruta de acceso del archivo sin formato o seleccione la variable que contiene el nombre de archivo.  
  
 **Opción de escritura**  
 Seleccione el método que va a utilizar para crear y escribir en el archivo.  
  
 **Generar un archivo sin formato inicial**  
 Haga clic en el botón para generar un archivo sin formato vacío que contenga solo las columnas (solo archivos de metadatos), sin tener que ejecutar el paquete. El archivo contiene las columnas seleccionadas en la página **Columnas:** del **Editor de destino de archivos sin formato**. Puede designar el origen de archivo sin formato para este archivo que solo tiene metadatos.  
  
 Al hacer clic en **Generar archivo sin formato inicial**, aparece un cuadro de mensaje. Haga clic en **Aceptar** para continuar con la creación del archivo. Haga clic en **Cancelar** para seleccionar otra lista de columnas en la página **Columnas:** .  
  
##  <a name="mapping"></a> Establecer las opciones de la pestaña Columnas  
 **Columnas de entrada disponibles**  
 Seleccione una o varias columnas de entrada para escribir en el archivo sin formato.  
  
 **Columna de entrada**  
 Una columna de entrada se agrega automáticamente a esta tabla cuando se selecciona en **Columnas de entrada disponibles**, o puede seleccionar la columna de entrada directamente en esta tabla.  
  
 **Alias de salida**  
 Especifique un nombre alternativo para usarlo en la columna de salida.  
  
## <a name="see-also"></a>Consulte también  
 [destino de archivo sin formato](data-flow/raw-file-destination.md)  
  
  
