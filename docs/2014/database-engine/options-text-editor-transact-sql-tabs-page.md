---
title: 'Opciones (Editor de texto-de Transact SQL: página de tabulaciones) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Tabs
dev_langs:
- TSQL
ms.assetid: a4499784-67f7-46ef-9f7c-2d0fdd117a52
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7dd6e11704497bd37fa4eb78948376587ece1119
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844759"
---
# <a name="options-text-editor---transact-sql---tabs-page"></a>Opciones (Editor de texto-de Transact SQL: página de pestañas)
  Utilice este cuadro de diálogo para cambiar el comportamiento de tabulación del Editor de consultas de [!INCLUDE[ssDE](../includes/ssde-md.md)] , que se utiliza para programar scripts de [!INCLUDE[tsql](../includes/tsql-md.md)] . Para mostrar estas opciones de configuración, haga clic en **Opciones** en el menú **Herramientas** , expanda la carpeta **Transact-SQL** , expanda la subcarpeta **SQL** y, a continuación, haga clic en **Tabulaciones**.  
  
## <a name="setting-options-in-multiple-locations"></a>Establecer opciones en varias ubicaciones  
 Las opciones del Editor de consultas de [!INCLUDE[ssDE](../includes/ssde-md.md)] también se pueden establecer en el cuadro de diálogo **Tabulaciones de Todos los lenguajes** . Si utiliza los cuadros de diálogo **Todos los lenguajes** para establecer diferentes opciones para los demás editores de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , como los editores MDX o DMX, debe restablecer las opciones del Editor de consultas del [!INCLUDE[ssDE](../includes/ssde-md.md)] mediante este cuadro de diálogo.  
  
## <a name="indenting"></a>Sangrías  
 **Ninguno**  
 Cuando se selecciona esta opción, no se aplica ninguna sangría a la nueva línea que se crea al presionar ENTRAR. El cursor se coloca en la primera columna de la nueva línea.  
  
 **Block**  
 Cuando se selecciona esta opción, se aplica una sangría de forma automática a la nueva línea que se crea al presionar ENTRAR, a la misma distancia que la línea anterior.  
  
 **Smart**  
 Esta opción no está disponible.  
  
## <a name="tabs"></a>Tabulaciones  
 **Tamaño de tabulación**  
 Establece la distancia en espacios entre las tabulaciones. El valor predeterminado es cuatro espacios.  
  
 **Tamaño de sangría**  
 Establece el tamaño en espacios de una sangría automática. El valor predeterminado es cuatro espacios. Se insertan caracteres de tabulación, de espacio o ambos para rellenar el tamaño especificado.  
  
 **Insertar espacios**  
 Cuando se selecciona esta opción, las operaciones de aplicación de sangrías solo insertan caracteres de espacio, pero no caracteres de tabulación. Si **Tamaño de sangría** se establece en 5, por ejemplo, se insertarán cinco espacios cada vez que se presione la tecla TAB o se haga clic en el botón **Aumentar sangría** en la barra de herramientas de la ventana principal de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] .  
  
 **Mantener tabulaciones**  
 Cuando se selecciona esta opción, las operaciones de aplicación de sangrías insertan todos los caracteres de tabulación posibles. Cada carácter de tabulación rellena el número de espacios especificados en **Tamaño de tabulación**. Si **Tamaño de sangría** no es un múltiplo par de **Tamaño de tabulación**, se agregarán caracteres de espacio para rellenar la diferencia.  
  
  
