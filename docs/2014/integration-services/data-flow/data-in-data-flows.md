---
title: Datos de flujos de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- comparing data
- data types [Integration Services], data flow
- parsing [Integration Services]
- string comparisons
- data flow [Integration Services], data options
ms.assetid: 8a9d6186-eb52-48e3-997e-021f24d458a3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9f7fe3638861d45e589f72871c10d6046436cb96
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781317"
---
# <a name="data-in-data-flows"></a>Datos de flujos de datos
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona un conjunto de tipos de datos que se usan en flujos de datos.  
  
## <a name="data-type-conversion"></a>Conversión de tipo de datos  
 El origen que se agrega a un flujo de datos convierte los datos de origen en tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Las transformaciones posteriores pueden convertir los datos en diferentes tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y, según el tipo de almacén de datos en el que se cargan los datos, los destinos pueden convertir el tipo de datos final de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el tipo de datos requerido por el almacén de datos de destino. Para obtener más información, vea [Integration Services Data Types](integration-services-data-types.md).  
  
 Para convertir los datos a un tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un componente de flujo de datos analiza los datos. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona dos tipos de análisis de datos: el análisis rápido y el análisis estándar. La mayoría de los componentes de flujo de datos puede usar solamente el análisis estándar. Sin embargo, el origen de archivo plano y la transformación Conversión de datos pueden usar el análisis rápido o estándar. Para más información, consulte [Parsing Data](parsing-data.md).  
  
## <a name="data-type-comparison"></a>Comparación de tipos de datos  
 Muchas transformaciones comparan valores de datos. Por ejemplo, la transformación Agregado compara valores con el fin de agregar valores en un conjunto de filas de datos, la transformación Ordenar compara valores para ordenarlos y la transformación Búsqueda compara valores con valores en una tabla de referencia independiente. Para especificar la forma en que se deben comparar las cadenas, la transformación incluye un conjunto de opciones de comparación, tales como pasar por alto la distinción entre mayúsculas y minúsculas, cómo tratar el tipo de escritura kana en un texto japonés, o si se deben omitir los caracteres de espacios en blanco en la cadena. Para más información, consulte [Comparing String Data](comparing-string-data.md).  
  
 El evaluador de expresiones también compara los valores de datos cuando evalúa las expresiones utilizadas por las variables, restricciones de precedencia y transformaciones.  
  
## <a name="data-flow-troubleshooting"></a>Solucionar problemas de flujo de datos  
 Una vez que ha implementado un paquete en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede analizar el flujo de datos en el paquete durante la ejecución para comprobar el rendimiento o buscar si hay algún otro problema. Hay informes estándar disponibles que le permiten ver el estado del paquete y el historial y consultar las vistas de la base de datos que proporcionan información detallada sobre la ejecución del paquete. También puede agregar y quitar dinámicamente las derivaciones de datos durante la ejecución de los componentes específicos de destino del paquete. Para obtener más información, consulte [Análisis de flujo de datos](data-flow.md).  
  
  
