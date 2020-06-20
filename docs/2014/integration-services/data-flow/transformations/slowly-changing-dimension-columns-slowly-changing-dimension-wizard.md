---
title: Columnas de dimensiones de variación lenta (Asistente para dimensiones de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 217f56bd035066797f156fdccedc901f10ceb312
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939336"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>Columnas de dimensión variable lenta (Asistente para dimensiones variables)
  Utilice el cuadro de diálogo **Columnas de dimensión variable** para seleccionar un tipo de cambio para cada una de las columnas de dimensión variable lenta.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de dimensión**  
 Seleccione una columna de dimensión de la lista.  
  
 **Tipo de cambio**  
 Seleccione un **Atributo fijo**o seleccione uno de los dos tipos de atributos variables. Utilice **Atributo fijo** cuando el valor de una columna no tenga que cambiar; [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tratará entonces los cambios como errores. Utilice **Atributo variable** para sobrescribir los valores existentes con los valores modificados. Utilice **Atributo histórico** para guardar los valores modificados en nuevos registros, al tiempo que los registros anteriores quedan marcados como desusados.  
  
 **Remove**  
 Seleccione una columna de dimensión y quítela de la lista de columnas asignadas haciendo clic en **Quitar**.  
  
## <a name="see-also"></a>Consulte también  
 [Configuración de salidas con el Asistente para dimensiones de variación lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
