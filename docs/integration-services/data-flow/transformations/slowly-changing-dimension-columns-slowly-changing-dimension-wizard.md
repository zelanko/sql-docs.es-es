---
description: Columnas de dimensión variable lenta (Asistente para dimensiones variables)
title: Columnas de dimensiones de variación lenta (Asistente para dimensiones de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8b27c9c0e575775449d2f3a25c5a20bd6667b5cd
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "88425727"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>Columnas de dimensión variable lenta (Asistente para dimensiones variables)

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilice el cuadro de diálogo **Columnas de dimensión variable** para seleccionar un tipo de cambio para cada una de las columnas de dimensión variable lenta.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de dimensión**  
 Seleccione una columna de dimensión de la lista.  
  
 **Tipo de cambio**  
 Seleccione un **Atributo fijo** o seleccione uno de los dos tipos de atributos variables. Utilice **Atributo fijo** cuando el valor de una columna no tenga que cambiar; [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tratará entonces los cambios como errores. Utilice **Atributo variable** para sobrescribir los valores existentes con los valores modificados. Utilice **Atributo histórico** para guardar los valores modificados en nuevos registros, al tiempo que los registros anteriores quedan marcados como desusados.  
  
 **Remove**  
 Seleccione una columna de dimensión y quítela de la lista de columnas asignadas haciendo clic en **Quitar**.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar salidas mediante el Asistente para dimensión de variación lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
