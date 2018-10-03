---
title: 'Opciones (Editor de texto: texto sin formato - página de tabulaciones) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.Tabs
ms.assetid: 07d82d10-bca9-4b37-abbb-58ef9bfb264b
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4025a4812b7bb284d5fdf0540491d1506f05cdea
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074776"
---
# <a name="options-text-editor---plain-text---tabs-page"></a>Options (Editor de texto - Texto sin formato - Página Pestañas)
  Utilice este cuadro de diálogo para cambiar el comportamiento del tabulador del Editor de texto que se usa para editar un documento que no esté asociado a ningún lenguaje de desarrollo específico. Para mostrar estas opciones de configuración, haga clic en **Opciones** en el menú **Herramientas** , expanda el **Editor de texto**, expanda **Texto sin formato**y, a continuación, haga clic en **Tabulaciones**.  
  
## <a name="setting-options-in-multiple-locations"></a>Establecer opciones en varias ubicaciones  
 Las opciones del Editor de texto sin formato también se pueden establecer en el cuadro de diálogo **Todos los idiomas General** . Si usa los cuadros de diálogos **Todos los lenguajes** con el fin de establecer diferentes opciones para los demás editores de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , como los editores MDX o DMX, debe restablecer las opciones del Editor de texto sin formato mediante este cuadro de diálogo.  
  
## <a name="indenting"></a>Sangrías  
 **Ninguno**  
 No aplica ninguna sangría a la nueva línea que se crea al presionar ENTRAR. El cursor se coloca en la primera columna de la nueva línea.  
  
 **Bloque**  
 Aplica una sangría a la nueva línea que se crea al presionar ENTRAR a la misma distancia a la que se creó la sangría de la línea anterior.  
  
 **Inteligente**  
 El editor de texto simple no admite este tipo de formato.  
  
## <a name="tabs"></a>Tabulaciones  
 **Tamaño de tabulación**  
 Establece la distancia en espacios entre las tabulaciones. El valor predeterminado es cuatro espacios.  
  
 **Tamaño de sangría**  
 Establece el tamaño en espacios de una sangría automática. El valor predeterminado es cuatro espacios. Se insertarán caracteres de tabulación, de espacio o ambos para rellenar el tamaño especificado.  
  
 **Insertar espacios**  
 Inserta únicamente caracteres de espacio, pero no inserta caracteres de tabulación, al aplicar sangrías. Si **Tamaño de sangría** se establece en 5, por ejemplo, se insertan cinco espacios cada vez que se presiona la tecla TAB o el botón **Aumentar sangría** en la barra de herramientas **Formato** .  
  
 **Mantener tabulaciones**  
 Inserta todos los caracteres de tabulación posibles al aplicar sangrías. Cada carácter de tabulación rellena el número de espacios especificados en **Tamaño de tabulación**. Si **Tamaño de sangría** no es un múltiplo par de **Tamaño de tabulación**, se agregarán caracteres de espacio para rellenar la diferencia.  
  
  
