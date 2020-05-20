---
title: Opciones (editor de texto-XML-Página formato) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97373178-d288-4127-af37-d9f5fe1b8607
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e0d36c5a92dba9f3f92943b65107e7eedb178554
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000637"
---
# <a name="options-text-editor---xml---formatting-page"></a>Opciones (Editor de texto - XML - Página Formato)

Este cuadro de diálogo permite especificar la configuración de formato del Editor XML. Puede tener acceso al cuadro de diálogo **Opciones** desde el menú **Herramientas**.  
  
> [!NOTE]  
> Esta configuración está disponible si selecciona la carpeta **Editor de texto**, la carpeta **XML** y, después, la opción **Formato** del cuadro de diálogo **Opciones**.  
  
## <a name="attributes"></a>Atributos  
 **Preservar el formato manual de atributos**  
 No vuelve a dar formato a los atributos. Este es el valor predeterminado.  
  
> [!NOTE]  
>  Si los atributos se encuentran en varias líneas, el editor sangra cada línea de atributos para que coincida con el sangrado del elemento primario.  
  
 **Alinear los atributos en líneas separadas**  
 Los atributos segundo y siguientes se alinean verticalmente para coincidir con el sangrado del primer atributo. El siguiente texto XML es un ejemplo de alineación de los atributos.  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95"  
</item>  
```  
  
## <a name="auto-reformat"></a>Formatear automáticamente  
 **Al pegar desde el portapapeles**  
 Vuelve a dar formato al texto XML pegado desde el portapapeles.  
  
 **Al terminar la etiqueta final**  
 Vuelve a dar formato al elemento cuando se completa la etiqueta final.  
  
## <a name="mixed-content"></a>Contenido mixto  
 **Formatear contenido mixto de forma predeterminada**  
 Intenta volver a dar formato al contenido mixto, excepto si se encuentra en un ámbito `xml:space="preserve"`. Este es el valor predeterminado.  
  
 Si un elemento contiene una mezcla de texto y marcado, el contenido se considera mixto. A continuación se incluye un ejemplo de un elemento con contenido mixto.  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
```  
  
 \</DIR>  
  
## <a name="see-also"></a>Consulte también  
 [Editor XML &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)  
