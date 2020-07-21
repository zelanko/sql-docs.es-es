---
title: Parametrizar (cuadro de diálogo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 50bd1674dcc31240864f87a6e0d13c2599996e0b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423532"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  El cuadro de diálogo **Parametrizar** permite asociar un parámetro nuevo o existente con una propiedad de una tarea. Abra el cuadro de diálogo haciendo clic con el botón secundario en una tarea o en la pestaña Flujo de control en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] y haciendo clic en **Parametrizar**. La siguiente lista describe los elementos de la interfaz de usuario en el cuadro de diálogo. Para más información sobre los parámetros, vea [Parámetros de Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="ui-element-list"></a>Lista de elementos de la interfaz de usuario  
 **Propiedad**  
 Seleccione la propiedad de la tarea que desea asociar con un parámetro. Esta lista se rellena con todas las propiedades que se pueden utilizar con parámetros.  
  
 **Usar parámetros existentes**  
 Seleccione esta opción para asociar la propiedad de tarea con un parámetro existente y, a continuación, seleccione el parámetro de la lista desplegable.  
  
 **No use parámetros**  
 Seleccione esta opción para quitar una referencia a un parámetro. Parámetro no se elimina.  
  
 **Crear nuevo parámetro**  
 Seleccione esta opción para crear un nuevo parámetro que desee asociar con la propiedad de tarea.  
  
 **Nombre**  
 Especifique el nombre del parámetro que desea crear.  
  
 **Descripción**  
 Especifique la descripción del parámetro.  
  
 **Valor**  
 Especifique el valor predeterminado del parámetro. Se conoce también como valor predeterminado de diseño, el cual se puede invalidar más adelante durante la fase de implementación.  
  
 **Ámbito**  
 Especifique el ámbito del parámetro seleccionando la opción **Proyecto** o **Paquete** . Los parámetros de proyecto se usan para proporcionar cualquier entrada externa que el proyecto recibe a uno o más paquetes del proyecto. Los parámetros de paquete permiten modificar la ejecución del paquete sin tener que modificarlo ni volver a implementarlo.  
  
 **Sensibilidad**  
 Especifique si es un parámetro con distinción activando o desactivando la casilla. Los valores de parámetros con distinción se cifran en el catálogo y aparecen como valor NULL cuando se ven con Transact-SQL o SQL Server Management Studio.  
  
 **Obligatoria**  
 Especifique si el parámetro requiere que se especifique un valor, distinto del valor predeterminado de diseño, antes de que el paquete se ejecute.  
  
## <a name="ui-element-list"></a>Lista de elementos de la interfaz de usuario  
  
