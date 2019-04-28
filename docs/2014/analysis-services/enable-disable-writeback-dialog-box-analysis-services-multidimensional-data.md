---
title: Habilitación y deshabilitación de cuadro de diálogo de reescritura (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitiondesigner.writebackenabledisable.f1
ms.assetid: 2d254393-3f0d-4b70-8b98-87159f9f3639
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6682d8ced6b80e12aea783857da548498641ddd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731507"
---
# <a name="enable-disable-writeback-dialog-box-analysis-services---multidimensional-data"></a>Habilitación y deshabilitación de cuadro de diálogo de reescritura (Analysis Services - datos multidimensionales)
  El cuadro de diálogo **Habilitar/deshabilitar reescritura** permite habilitar o deshabilitar la reescritura para un grupo de medida en un cubo. Al habilitar la reescritura en un grupo de medida se define una partición de reescritura y se crea una tabla de reescritura para ese grupo de medida. Al deshabilitar la reescritura en un grupo de medida se quita la partición de reescritura, pero no se elimina la tabla de reescritura a fin de evitar la pérdida imprevista de datos. Para mostrar el cuadro de diálogo **Habilitar/deshabilitar reescritura** :  
  
-   En el Diseñador de cubos, haga clic en **Configuración de reescritura** (en el panel **Grupos de medida** de la pestaña **Particiones** ).  
  
-   En el Diseñador de cubos, haga clic con el botón derecho en una partición de la cuadrícula **Particiones** (en el panel **Grupos de medida** de la pestaña **Particiones** ) y, después, seleccione **Configuración de reescritura** en el menú contextual.  
  
## <a name="options"></a>Opciones  
 **Nombre de la tabla**  
 Escriba el nombre de la tabla de reescritura que desea crear para la partición seleccionada. La tabla de escritura diferida almacena los cambios realizados al grupo de medidas desde una aplicación cliente.  
  
> [!NOTE]  
>  Esta opción está deshabilitada si la reescritura no está habilitada.  
  
 **Origen de datos**  
 Seleccione el origen de datos que contendrá la tabla de reescritura.  
  
> [!NOTE]  
>  Esta opción está deshabilitada si la reescritura no está habilitada.  
  
 **Nueva**  
 Haga clic para mostrar el cuadro de diálogo **Administrador de conexiones** y defina un nuevo origen de datos para que contenga la tabla de reescritura.  
  
> [!NOTE]  
>  Esta opción está deshabilitada si la reescritura no está habilitada.  
  
  
