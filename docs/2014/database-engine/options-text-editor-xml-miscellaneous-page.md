---
title: Opciones (Editor de texto - XML - página de varios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 1a9509f0-c663-4b31-b396-7f5dc4371651
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 70689ff767661409dce982d7bb294d0b620838e2
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328435"
---
# <a name="options-text-editor---xml---miscellaneous-page"></a>Opciones (Editor de texto - XML - Página Varios)

El cuadro de diálogo **Opciones** permite modificar las opciones de finalización automática y esquema del Editor XML. Estas opciones se encuentran disponibles cuando, en el menú **Herramientas** , se hace clic en **Opciones**, se expande la carpeta **Editor de texto** , se hace clic en **XML** y después se selecciona **Varios** .  
  
## <a name="auto-insert"></a>Inserción automática  
 **Etiquetas de cierre**  
 El Editor de texto agrega etiquetas de cierre al crear elementos XML. Si se selecciona la etiqueta de inicio de un elemento, el editor inserta la etiqueta de cierre correspondiente, incluido el prefijo de espacio de nombres. Esta casilla está activada de forma predeterminada.  
  
 **Comillas de atributo**  
 Al crear atributos XML, el editor inserta los caracteres `="``"` y coloca el símbolo de intercalación (**^)** dentro de las comillas. Esta casilla está activada de forma predeterminada.  
  
 **Declaraciones de Namespace**  
 El editor inserta automáticamente declaraciones de espacios de nombres cuando son necesarias. Esta casilla está activada de forma predeterminada.  
  
 **Otro marcado (comentarios, CDATA)**  
 Finalización automática de comentarios, CDATA, DOCTYPE, instrucciones de proceso y otro tipo de marcado. Esta casilla está activada de forma predeterminada.  
  
## <a name="network"></a>red  
 **Descargar automáticamente DTD y esquemas**  
 Los esquemas y las definiciones de tipos de documentos (DTD) se descargan automáticamente desde ubicaciones HTTP. Esta función utiliza System.Net con la opción de detección de servidores proxy automáticos habilitada. Esta casilla está activada de forma predeterminada.  
  
## <a name="outlining"></a>Esquematización  
 **Especificar el modo de esquematización al abrirán archivos**  
 Activa la función de esquematización al abrir un archivo. Esta casilla está activada de forma predeterminada.  
  
## <a name="caching"></a>Almacenamiento en memoria caché  
 **Esquemas**  
 Especifica la ubicación de la caché de esquemas. El botón Examinar (...) abre la ubicación de la caché de esquemas actual en una ventana nueva. La ubicación predeterminada es  *\<directorio de instalación de Management Studio >* \Xml\Schemas.  
