---
title: 'Opciones (editor de texto: XML: Página tabulaciones) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Tabs
ms.assetid: 13bf5f8c-aba3-4c05-b8bb-eb475797c9bd
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 01721e60e2f70462d606586225ab98329dad7daa
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000611"
---
# <a name="options-text-editorxmltabs-page"></a>Opciones (Editor de texto: XML: página Pestañas)
  Este cuadro de diálogo permite cambiar el comportamiento del tabulador del Editor XML, que se usa para editar documentos XML. Para mostrar estas opciones de configuración, haga clic en **Opciones** en el menú **Herramientas** , expanda la carpeta **Editor de texto** , expanda la subcarpeta **XML** y, a continuación, haga clic en **Tabulaciones**.  
  
## <a name="setting-options-in-multiple-locations"></a>Establecer opciones en varias ubicaciones  
 Las opciones del Editor XML también se pueden establecer en el cuadro de diálogo **Todos los idiomas** de la página General. Si usa los cuadros de diálogo **todos los lenguajes** para establecer diferentes opciones para los demás [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] editores, como los editores de DMX o MDX, debe restablecer las opciones del editor XML mediante este cuadro de diálogo.  
  
## <a name="indenting"></a>Sangrías  
 **Ninguno**  
 Cuando se selecciona esta opción, no se aplica ninguna sangría a la nueva línea que se crea al presionar ENTRAR. El cursor se coloca en la primera columna de la nueva línea.  
  
 **Bloquear**  
 Cuando se selecciona esta opción, se aplica una sangría de forma automática a la nueva línea que se crea al presionar ENTRAR, a la misma distancia que la línea anterior.  
  
 **Automática**  
 Cuando se selecciona esta opción, la nueva línea que se crea al presionar ENTRAR se coloca conforme al contexto. Por ejemplo, después de una llave de apertura ({), se aplicará automáticamente una sangría con una tabulación adicional a las líneas incluidas. La llave de cierre (}) se volverá a alinear con la llave de apertura correspondiente.  
  
## <a name="tabs"></a>Tabulaciones  
 **Tamaño de tabulación**  
 Establece la distancia en espacios entre las tabulaciones. El valor predeterminado es cuatro espacios.  
  
 **Tamaño de sangría**  
 Establece el tamaño en espacios de una sangría automática. El valor predeterminado es cuatro espacios. Se insertan caracteres de tabulación, de espacio o ambos para rellenar el tamaño especificado.  
  
 **Insertar espacios**  
 Cuando se selecciona esta opción, las operaciones de aplicación de sangrías solo insertan caracteres de espacio, pero no caracteres de tabulación. Si **tamaño de sangría** se establece en 5, por ejemplo, se insertarán cinco caracteres de espacio cada vez que se presione la tecla TAB o se haga clic en el botón **aumentar sangría** en la barra de herramientas de la [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ventana principal.  
  
 **Mantener tabulaciones**  
 Cuando se selecciona esta opción, las operaciones de aplicación de sangrías insertan todos los caracteres de tabulación posibles. Cada carácter de tabulación rellena el número de espacios especificados en **Tamaño de tabulación**. Si **Tamaño de sangría** no es un múltiplo par de **Tamaño de tabulación**, se agregarán caracteres de espacio para rellenar la diferencia.  
  
  
