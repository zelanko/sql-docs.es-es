---
description: Informe de evaluación (AccessToSQL)
title: Informe de evaluación (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6c747f50c9216626e710318175cf5e53a0624d7a
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987661"
---
# <a name="assessment-report-accesstosql"></a>Informe de evaluación (AccessToSQL)
La ventana Informe de evaluación muestra los resultados de la conversión de objetos de base de datos a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis y también puede ayudarle a calcular la complejidad y el costo de los proyectos de migración.  
  
Para crear un informe de evaluación, seleccione los objetos que desea convertir en el explorador de metadatos de origen, haga clic con el botón derecho en **bases**de datos y, a continuación, seleccione **crear informe**. También puede mostrar este informe automáticamente después de convertir los esquemas. Sin embargo, el nombre del informe será informe de conversión. Para obtener más información, vea [configuración del proyecto (GUI) (SSMA Common)](../sybase/project-settings-gui-sybasetosql.md).  
  
## <a name="options"></a>Opciones  
**Panel Explorador**  
Contiene una jerarquía de objetos en el informe de evaluación. Expanda carpetas para ver objetos y subcomponentes individuales. Al hacer clic en una categoría o un objeto, las estadísticas de conversión de esa categoría u objeto aparecen en el panel de detalles.  
  
**Panel de detalles**  
Muestra estadísticas de conversión o mensajes de error y advertencia para el objeto seleccionado. Por ejemplo, si se selecciona la carpeta tablas, el panel detalles mostrará los números de claves externas, índices, claves principales y tablas que se han convertido.  
  
**Panel Mensajes**  
Muestra los errores, las advertencias y los mensajes de información que se generaron cuando se creó el informe de evaluación. Los mensajes se agrupan por número.  
  
Para ver los detalles del mensaje, haga clic en **errores**, **advertencias**o **mensajes**y, a continuación, expanda un mensaje. SSMA mostrará la lista de objetos que tienen este error. Haga clic en un objeto para mostrar todos los detalles de conversión del objeto.  
  
## <a name="see-also"></a>Consulte también  
[Referencia de la interfaz de usuario (acceso)](./user-interface-reference-accesstosql.md)  
