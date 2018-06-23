---
title: Editor de destino de archivo sin formato (página columnas) | Documentos de Microsoft
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
- sql12.dts.designer.rawfiledestinationcolumns.f1
ms.assetid: 37f61d0b-1269-42ee-94ab-011cbaac63e9
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4cf6ab3dea83b4f6dc575f4d32af04d9994d04df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104726"
---
# <a name="raw-file-destination-editor-columns-page"></a>Editor de destino de archivo sin formato (página Columnas)
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
 Haga clic en el botón para generar un archivo sin formato vacío que contenga solo las columnas (solo archivos de metadatos), sin tener que ejecutar el paquete. Puede designar el origen de archivo sin formato para el archivo que solo tiene metadatos.  
  
 Al hacer clic en el botón, aparece una lista de columnas. Puede hacer clic en Cancelar y modificar las columnas, o hacer clic en Aceptar y continuar con la creación del archivo.  
  
##  <a name="mapping"></a> Establecer las opciones de la pestaña Columnas  
 **Columnas de entrada disponibles**  
 Seleccione una o varias columnas de entrada para escribir en el archivo sin formato.  
  
 **Columna de entrada**  
 Una columna de entrada se agrega automáticamente a esta tabla cuando se selecciona en **Columnas de entrada disponibles**, o puede seleccionar la columna de entrada directamente en esta tabla.  
  
 **Alias de salida**  
 Especifique un nombre alternativo para usarlo en la columna de salida.  
  
## <a name="see-also"></a>Vea también  
 [Destino de archivo sin formato](data-flow/raw-file-destination.md)  
  
  