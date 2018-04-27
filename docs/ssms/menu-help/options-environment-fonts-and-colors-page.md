---
title: Opciones (Entorno - página Fuentes y colores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-menu
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Environment.Fonts_And_Colors
- VS.TOOLSOPTIONSPAGES.ENVIRONMENT.FONTS_AND_COLORS
ms.assetid: ea3aa222-538d-485f-99dc-01eb02cdcfea
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 009dd31848b47c29ce44422a4cb9f73d2ef39768
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="options-environment---fonts-and-colors-page"></a>Opciones (Entorno -página Fuentes y colores)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
El cuadro de diálogo **Opciones[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] le permite establecer una combinación personalizada de fuentes y colores para diversos elementos de la interfaz de usuario de**  [!INCLUDE[msCoName](../../includes/msconame_md.md)]. En el menú **Herramientas**, haga clic en **Opciones**, expanda la carpeta **Entorno** y seleccione **Fuentes y colores**.  
  
Los cambios en la combinación de colores no surtirán efecto durante la sesión en la que los realice. Puede evaluar los cambios de color abriendo otra instancia de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] y creando las condiciones bajo las cuales espera que se apliquen los cambios.  
  
## <a name="uielement-list"></a>Lista de UIElement  
**Mostrar valores para**  
Muestra todos los elementos de la interfaz de usuario en los que puede modificar combinaciones de fuentes y colores. Después de seleccionar un elemento de esta lista puede personalizar la configuración del color para el elemento seleccionado en **Mostrar los elementos**.  
  
|Término|Definición|  
|--------|--------------|  
|Editor de texto|Los cambios en la configuración del estilo, tamaño y color de fuente para el Editor de texto afectan a la apariencia del editor de texto predeterminado. Los documentos abiertos en un editor de texto fuera de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] no afectarán a esta configuración.|  
|Impresora|Los cambios en la configuración del estilo, tamaño y color de fuente para la impresora afectan a la apariencia del texto de los documentos impresos.<br /><br />Nota: Puede seleccionar una fuente predeterminada para imprimir distinta a la que se usa para la visualización en el Editor de texto. Esta opción puede ser útil para imprimir código que contenga caracteres de un solo byte o de doble byte.|  
|[Todas las ventanas de herramientas de texto **]**|Los cambios en la configuración del estilo, tamaño y color de fuente para este elemento afectan a la apariencia del texto de las ventanas de herramientas que tienen paneles de resultados en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Por ejemplo, ventana Resultados, ventana TextResults, etc.<br /><br />Nota: Los cambios en el texto de los elementos [Todas las ventanas de herramientas de texto] no surten efecto durante la sesión en la que se realizan. Puede evaluar dichos cambios abriendo otra instancia de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].|  
|Ventana Resultados de la búsqueda|Los cambios en la configuración del estilo, tamaño y color de fuente para este elemento afectan a la apariencia del texto de la ventana FindResults.|  
|Resultados (ventana)|Los cambios en la configuración del estilo, tamaño y color de fuente para este elemento afectan a la apariencia del texto de la ventana Resultados.|  
|Resultados de la cuadrícula|Los cambios en la configuración del estilo, tamaño y color de fuente para este elemento afectan a la apariencia del texto del área **Resultados de la cuadrícula** de la ventana Consultar.|  
|Plan de ejecución|Los cambios en la configuración del estilo, tamaño y color de fuente para este elemento afectan a la apariencia del texto en el plan de ejecución de las consultas de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y [!INCLUDE[ssEW](../../includes/ssew_md.md)] .|  
|Resultados del texto|Los cambios en la configuración del estilo, tamaño y color de fuente para este elemento afectan a la apariencia del texto del área **Resultados del texto** de la ventana de consulta.|  
|Diseñadores de Business Intelligence|Los cambios en la configuración del estilo de fuente, tamaño y color de fuente para este elemento afectan a la apariencia del texto de la ventana BusinessIntelligenceDesigners.|  
  
**Usar predeterminados**  
El botón **Usar predeterminados** restablece el valor de los valores de fuente y color predeterminados del elemento de la lista que haya seleccionado en la lista **Mostrar valores para** .  
  
**Fuente (los tipos en negrita indican fuentes con ancho fijo)**  
Enumera todas las fuentes instaladas en el sistema. Al abrir por primera vez esta lista desplegable, se selecciona la fuente actual para el elemento seleccionado en la lista **Mostrar valores para** . Las fuentes fijas (que son más fáciles de alinear en un editor) aparecen en negrita.  
  
**Tamaño**  
Muestra los tamaños de punto disponibles para la fuente seleccionada. El cambio en el tamaño de la fuente afecta a todas las entradas de **Mostrar los elementos** de una selección de **Mostrar valores para** .  
  
**Mostrar los elementos**  
Muestra los elementos en los que puede modificar el color de primer plano y de fondo.  
  
> [!NOTE]  
> **E**l elemento predeterminado es Texto. De esta forma, las propiedades asignadas a Texto serán reemplazadas por las propiedades asignadas a otros elementos de muestra. Por ejemplo, si asigna el color azul a **Texto** y el color verde a Identificador, todos los identificadores aparecerán en verde. En este ejemplo, las propiedades de Identificador reemplazan a las propiedades de Texto.  
  
Algunos elementos de muestra son los siguientes:  
  
-   Margen del indicador: margen situado a la izquierda del Editor de código en el que aparecen los iconos de marcadores y puntos de interrupción.  
  
-   Texto contraíble: bloque de texto o código que se puede cambiar dentro y fuera de la vista del CodeEditor (solo XML).  
  
**Primer plano del elemento**  
Muestra los colores disponibles que puede elegir para el primer plano del elemento seleccionado en **Mostrar los elementos**. Puesto que algunos elementos están relacionados, debe mantenerse una combinación de visualización coherente; por ejemplo, al cambiar el color de primer plano del texto también cambiará el color de primer plano de elementos como Cadena.  
  
**Custom**  
Muestra el cuadro de diálogo **Color** , en el que se establece un color personalizado para el elemento seleccionado en la lista **Mostrar los elementos** .  
  
> [!NOTE]  
> La posibilidad de definir colores personalizados puede estar limitada por la configuración del color de la pantalla del equipo. Por ejemplo, si el equipo está configurado para mostrar 256 colores y selecciona un color personalizado en el cuadro de diálogo **Color[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)],**  elegirá como predeterminado el valor disponible de **Colores básicos** que más se aproxime, y mostrará el color negro en el cuadro de diálogo **Color**.  
  
**Fondo del elemento**  
Proporciona una paleta de colores de la que puede elegir un color de fondo para el elemento seleccionado en **Mostrar los elementos**. Puesto que algunos elementos están relacionados, debe mantenerse una combinación de visualización coherente; por ejemplo, al cambiar el color de fondo del texto también cambiará el color de fondo de elementos como Cadena.  
  
**Personalizado**  
Muestra el cuadro de diálogo **Color** , en el que se establece un color personalizado para el elemento seleccionado en la lista **Mostrar los elementos** .  
  
**Negrita**  
Seleccione esta casilla para mostrar el texto de los displayitems seleccionados en negrita. El texto en negrita es más fácil de identificar en un editor.  
  
**Ejemplo**  
Muestra un ejemplo de la combinación de estilo, tamaño y color de fuente para los valores seleccionados en **Mostrar valores para** y **Mostrar los elementos**. Puede utilizar este cuadro de texto para mostrar una vista previa de los resultados a medida que experimente con opciones de formatos diferentes.  
  
## <a name="see-also"></a>Ver también  
[Codificación de colores en los editores de código](http://msdn.microsoft.com/en-us/802882dc-c997-4e3f-8a01-994bb43169ae)  
[Opciones (pestaña Editor de texto/Editor y página Barra de estado)](http://msdn.microsoft.com/en-us/e4815678-7885-4631-878f-c6a2b857ee05)  
  
