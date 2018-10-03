---
title: Flat File Connection Manager Editor (página columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ffileconnection.columns.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 40ce7537-abd0-4973-97fd-6ccb90fddfa0
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a7aed741e639fe76fe1565c10e203e0871929863
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123887"
---
# <a name="flat-file-connection-manager-editor-columns-page"></a>Editor del administrador de conexiones de archivos planos (página Columnas)
  Utilice la página **Columnas** del cuadro de diálogo **Editor del administrador de conexiones de archivos planos** para especificar la información de filas y columnas, y para obtener una vista previa del archivo.  
  
 Para obtener más información acerca del administrador de conexiones de archivos planos, vea [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de archivo plano en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
## <a name="flat-file-format-dynamic-options"></a>Opciones dinámicas de formato para archivos planos  
  
### <a name="format--delimited"></a>Formato = Delimitado  
 **Delimitador de filas**  
 Selecciónelo de la lista de delimitadores de filas disponibles o escriba el texto delimitador.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|Las filas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las filas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las filas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las filas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las filas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las filas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las filas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las filas se delimitan mediante una barra vertical.|  
  
 **Delimitador de columna**  
 Selecciónelo de la lista de delimitadores de columna disponibles o escriba el texto delimitador.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las columnas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las columnas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las columnas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las columnas se delimitan mediante un punto y coma.|  
|**Coma {,}**|Las columnas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las columnas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las columnas se delimitan mediante una barra vertical.|  
  
 **Actualizar**  
 Al hacer clic en **Actualizar**, verá el efecto del cambio de delimitadores que se van a omitir. Este botón solo se hace visible después de cambiar otras opciones de conexión.  
  
 **Vista previa de filas**  
 Presenta datos de ejemplo del archivo plano, divididos en columnas y filas mediante las opciones seleccionadas.  
  
 **Restablecer columnas**  
 Al hacer clic en **Restablecer columnas**se eliminará todo, excepto las columnas originales.  
  
### <a name="format--fixed-width"></a>Formato = Ancho fijo  
 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de color rojo de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Ancho de fila**  
 Especifique la longitud de la fila antes de agregar los delimitadores para las columnas individuales. O bien arrastre la línea roja vertical en la ventana de vista previa para marcar el final de la fila. El valor del ancho de la fila se actualizará automáticamente.  
  
 **Restablecer columnas**  
 Al hacer clic en **Restablecer columnas**se eliminará todo, excepto las columnas originales.  
  
### <a name="format--ragged-right"></a>Formato = Derecho irregular  
  
> [!NOTE]  
>  Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.  
  
 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de color rojo de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Delimitador de filas**  
 Selecciónelo de la lista de delimitadores de filas disponibles o escriba el texto delimitador.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|Las filas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las filas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las filas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las filas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las filas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las filas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las filas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las filas se delimitan mediante una barra vertical.|  
  
 **Restablecer columnas**  
 Al hacer clic en **Restablecer columnas**se eliminará todo, excepto las columnas originales.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor del Administrador de conexiones de archivos planos &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor del Administrador de conexiones de archivos planos &#40;página Opciones avanzadas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  
