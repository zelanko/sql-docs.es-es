---
title: 'Opciones (Editor de texto: XML - página formato) | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Formatting
ms.assetid: 97373178-d288-4127-af37-d9f5fe1b8607
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5d77f7351d712f63e9cfc92c3ff03b131cb6d5d3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104763"
---
# <a name="options-text-editor---xml---formatting-page"></a>Opciones (Editor de texto - XML - Página Formato)
  Este cuadro de diálogo permite especificar la configuración de formato del Editor XML. Puede tener acceso al cuadro de diálogo **Opciones** desde el menú **Herramientas**.  
  
> [!NOTE]  
>  Esta configuración está disponible si selecciona la carpeta **Editor de texto**, la carpeta **XML** y, después, la opción **Formato** del cuadro de diálogo **Opciones**.  
  
## <a name="attributes"></a>Atributos  
 **Preservar el formato manual de atributos**  
 No vuelve a dar formato a los atributos. Ésta es la opción predeterminada.  
  
> [!NOTE]  
>  Si los atributos se encuentran en varias líneas, el editor sangra cada línea de atributos para que coincida con el sangrado del elemento primario.  
  
 **Alinear los atributos en una línea independiente**  
 Los atributos segundo y siguientes se alinean verticalmente para coincidir con el sangrado del primer atributo. El siguiente texto XML es un ejemplo de alineación de los atributos.  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95"  
</item>  
```  
  
## <a name="auto-reformat"></a>Formatear automáticamente  
 **Al pegar desde el Portapapeles.**  
 Vuelve a dar formato al texto XML pegado desde el portapapeles.  
  
 **En la realización de la etiqueta de cierre**  
 Vuelve a dar formato al elemento cuando se completa la etiqueta final.  
  
## <a name="mixed-content"></a>Contenido mixto  
 **Formatear contenido mixto de forma predeterminada.**  
 Intenta volver a dar formato al contenido mixto, excepto si se encuentra en un ámbito `xml:space="preserve"`. Ésta es la opción predeterminada.  
  
 Si un elemento contiene una mezcla de texto y marcado, el contenido se considera mixto. A continuación se incluye un ejemplo de un elemento con contenido mixto.  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
```  
  
 \</ dir >  
  
## <a name="see-also"></a>Vea también  
 [Editor XML &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)  
  
  