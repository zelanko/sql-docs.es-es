---
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c28fb4cf5d110e01b156fc6ce985b2cb2fb7bfe1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910685"
---
# <a name="assessment-report-accesstosql"></a>Informe de evaluación (AccessToSQL)
La ventana Informe de evaluación muestra los resultados de la conversión de objetos de [!INCLUDE[tsql](../../includes/tsql-md.md)] base de datos a sintaxis y también puede ayudarle a calcular la complejidad y el costo de los proyectos de migración.  
  
Para crear un informe de evaluación, seleccione los objetos que desea convertir en el explorador de metadatos de origen, haga clic con el botón derecho en **bases**de datos y, a continuación, seleccione **crear informe**. También puede mostrar este informe automáticamente después de convertir los esquemas. Sin embargo, el nombre del informe será informe de conversión. Para obtener más información, vea [configuración del proyecto (GUI) (SSMA Common)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
## <a name="options"></a>Opciones  
**Panel Explorador**  
Contiene una jerarquía de objetos en el informe de evaluación. Expanda carpetas para ver objetos y subcomponentes individuales. Al hacer clic en una categoría o un objeto, las estadísticas de conversión de esa categoría u objeto aparecen en el panel de detalles.  
  
**Panel de detalles**  
Muestra estadísticas de conversión o mensajes de error y advertencia para el objeto seleccionado. Por ejemplo, si se selecciona la carpeta tablas, el panel detalles mostrará los números de claves externas, índices, claves principales y tablas que se han convertido.  
  
**Panel Mensajes**  
Muestra los errores, las advertencias y los mensajes de información que se generaron cuando se creó el informe de evaluación. Los mensajes se agrupan por número.  
  
Para ver los detalles del mensaje, haga clic en **errores**, **advertencias**o **mensajes**y, a continuación, expanda un mensaje. SSMA mostrará la lista de objetos que tienen este error. Haga clic en un objeto para mostrar todos los detalles de conversión del objeto.  
  
## <a name="see-also"></a>Consulte también  
[Referencia de la interfaz de usuario (acceso)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
