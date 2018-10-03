---
title: Cuadro de diálogo se parametrizan | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76a48abe8ab2fe8481b2944ed6b3c77258b4c855
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075623"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  El cuadro de diálogo **Parametrizar** permite asociar un parámetro nuevo o existente con una propiedad de una tarea. Abra el cuadro de diálogo haciendo clic con el botón secundario en una tarea o en la pestaña Flujo de control en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] y haciendo clic en **Parametrizar**. La siguiente lista describe los elementos de la interfaz de usuario en el cuadro de diálogo. Para más información sobre los parámetros, vea [Parámetros de Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Propiedad**  
 Seleccione la propiedad de la tarea que desea asociar con un parámetro. Esta lista se rellena con todas las propiedades que se pueden utilizar con parámetros.  
  
 **Usar parámetro existente**  
 Seleccione esta opción para asociar la propiedad de tarea con un parámetro existente y, a continuación, seleccione el parámetro de la lista desplegable.  
  
 **No usar el parámetro**  
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
  
 **Con distinción**  
 Especifique si es un parámetro con distinción activando o desactivando la casilla. Los valores de parámetros con distinción se cifran en el catálogo y aparecen como valor NULL cuando se ven con Transact-SQL o SQL Server Management Studio.  
  
 **Obligatorio**  
 Especifique si el parámetro requiere que se especifique un valor, distinto del valor predeterminado de diseño, antes de que el paquete se ejecute.  
  
## <a name="uielement-list"></a>Lista de UIElement  
  
