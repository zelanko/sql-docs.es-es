---
title: 'Opciones (Editor de texto - todos los idiomas: página tabulaciones) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.All_Languages.Tabs
ms.assetid: bd715d6b-f873-41d4-aa10-57b7098b61cc
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f3e0df6dced5c69f60cbb95abcb5ba8eee78879b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198253"
---
# <a name="options-text-editor---all-languages--tabs-page"></a>Opciones (Editor de texto - todos los idiomas: página tabulaciones)
  Utilice este cuadro de diálogo para establecer el comportamiento de tabulación en los cinco editores de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para mostrar estas opciones, haga clic en **Opciones** en el menú **Herramientas** . Seleccione la carpeta **Editor de texto**, expanda la carpeta **Todos los lenguajes** y haga clic en **Tabulaciones**.  
  
## <a name="tabbing-options-by-editor"></a>Opciones de tabulación por editor  
 Debe usar los cuadros de diálogo de **Todos los lenguajes** para establecer las opciones de los editores DMX, MDX y SQL Server Compact. Las opciones establecidas aquí también se aplican al texto simple, a Transact-SQL y a los editores XML, pero puede establecer opciones por separado para esos editores si expande las subcarpetas correspondientes a esos idiomas y selecciona sus páginas de opciones. Algunos lenguajes no admiten todas las opciones de tabulación.  
  
> [!CAUTION]  
>  Si establece la opción usar este cuadro de diálogo, pero quiere un valor diferente para el texto simple, Transact-SQL o el editor XML, debe establecer las opciones de esos editores después de aplicar las opciones seleccionadas en el cuadro de diálogo **Todos los lenguajes**.  
  
 El mensaje "Los valores de la sangría (o del tabulador) para formatos de texto individuales están en conflicto entre sí" aparece si se han seleccionado diferentes valores para determinados editores. Por ejemplo, este mensaje aparece si la opción **Bloque** está seleccionada en **Texto simple**, pero se ha seleccionado **Ninguna** en **XML**.  
  
## <a name="indenting"></a>Sangrías  
 **Ninguno**  
 Cuando se selecciona esta opción, no se aplica ninguna sangría a la nueva línea que se crea al presionar ENTRAR. El cursor se coloca en la primera columna de la nueva línea.  
  
 **bloque**  
 Cuando se selecciona esta opción, se aplica una sangría de forma automática a la nueva línea que se crea al presionar ENTRAR, a la misma distancia que la línea anterior.  
  
 **Inteligente**  
 Cuando se selecciona esta opción, la nueva línea que se crea al presionar ENTRAR se coloca conforme al contexto.  
  
## <a name="tabs"></a>Tabulaciones  
 **Tamaño de tabulación**  
 Establece la distancia en espacios entre las tabulaciones. El valor predeterminado es cuatro espacios.  
  
 **Tamaño de sangría**  
 Establece el tamaño en espacios de una sangría automática. El valor predeterminado es cuatro espacios. Se insertarán caracteres de tabulación, de espacio o ambos para rellenar el tamaño especificado.  
  
 **Insertar espacios**  
 Cuando se selecciona esta opción, las operaciones de aplicación de sangrías solo insertan caracteres de espacio, pero no caracteres de tabulación. Si **Tamaño de sangría** se establece en 5, por ejemplo, se insertarán cinco espacios cada vez que se pulse la tecla TAB o se haga clic en el botón **Aumentar sangría** en la barra de herramientas de la ventana principal de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 **Mantener tabulaciones**  
 Cuando se selecciona esta opción, las operaciones de aplicación de sangrías insertan todos los caracteres de tabulación posibles. Cada carácter de tabulación rellena el número de espacios especificados en **Tamaño de tabulación**. Si **Tamaño de sangría** no es un múltiplo par de **Tamaño de tabulación**, se agregarán caracteres de espacio para rellenar la diferencia.  
  
  