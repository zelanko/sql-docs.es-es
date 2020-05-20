---
title: Opciones (editor de texto-XML-Página varios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 1a9509f0-c663-4b31-b396-7f5dc4371651
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 51ad78c95881daacebcb3f2b7999a299cd4ebd7d
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000595"
---
# <a name="options-text-editor---xml---miscellaneous-page"></a>Opciones (Editor de texto - XML - Página Varios)

El cuadro de diálogo **Opciones** permite modificar las opciones de finalización automática y esquema del Editor XML. Estas opciones se encuentran disponibles cuando, en el menú **Herramientas** , se hace clic en **Opciones**, se expande la carpeta **Editor de texto** , se hace clic en **XML** y después se selecciona **Varios** .  
  
## <a name="auto-insert"></a>Inserción automática  
 **Etiquetas de cierre**  
 El Editor de texto agrega etiquetas de cierre al crear elementos XML. Si se selecciona la etiqueta de inicio de un elemento, el editor inserta la etiqueta de cierre correspondiente, incluido el prefijo de espacio de nombres. Esta casilla está activada de forma predeterminada.  
  
 **Comillas de atributos**  
 Al crear atributos XML, el editor inserta los caracteres `="``"` y coloca el símbolo de intercalación (**^)** dentro de las comillas. Esta casilla está activada de forma predeterminada.  
  
 **Declaraciones de espacio de nombres**  
 El editor inserta automáticamente declaraciones de espacios de nombres cuando son necesarias. Esta casilla está activada de forma predeterminada.  
  
 **Otro tipo de marcado (Comentarios, CDATA)**  
 Finalización automática de comentarios, CDATA, DOCTYPE, instrucciones de proceso y otro tipo de marcado. Esta casilla está activada de forma predeterminada.  
  
## <a name="network"></a>Red  
 **Descargar automáticamente DTD y esquemas**  
 Los esquemas y las definiciones de tipos de documentos (DTD) se descargan automáticamente desde ubicaciones HTTP. Esta función utiliza System.Net con la opción de detección de servidores proxy automáticos habilitada. Esta casilla está activada de forma predeterminada.  
  
## <a name="outlining"></a>esquematizar  
 **Especificar el modo de esquematización al abrir los archivos**  
 Activa la función de esquematización al abrir un archivo. Esta casilla está activada de forma predeterminada.  
  
## <a name="caching"></a>Almacenamiento en memoria caché  
 **Esquemas**  
 Especifica la ubicación de la caché de esquemas. El botón Examinar (...) abre la ubicación de la caché de esquemas actual en una ventana nueva. La ubicación predeterminada es * \< Management Studio directorio de instalación>* \Xml\Schemas.  
