---
title: Definir claves principales lógicas en una vista del origen de datos (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90684f55414fa9e3f0d68a8ec90884fdae4d2c0a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="define-logical-primary-keys-in-a-data-source-view-analysis-services"></a>Definir claves principales lógicas en una vista del origen de datos (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El Asistente para vistas del origen de datos y el Diseñador de vistas del origen de datos definen automáticamente una clave principal para una tabla que se agrega a una vista del origen de datos basada en una tabla de base de datos subyacente.  
  
 En ocasiones, podría ser necesario definir manualmente una clave principal en la vista del origen de datos. Por ejemplo, por motivos de rendimiento o diseño, es posible que las tablas de un origen de datos no tengan definidas de forma explícita columnas de clave principal. Las consultas con nombre y las vistas también pueden pasar por alto la columna de clave principal de una tabla. Si una tabla, vista o consulta con nombre no tiene definida una clave principal física, puede definir manualmente una clave principal lógica en la tabla, vista o consulta con nombre en el Diseñador de vistas del origen de datos.  
  
## <a name="set-a-logical-primary-key"></a>Establecer una clave principal lógica  
 La claves principales son necesarias en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para identificar de manera exclusiva los registros de una tabla, identificar las columnas de clave en las tablas de dimensiones y admitir relaciones entre tablas, vistas y consultas con nombre. Estas relaciones se usan para crear consultas para la recuperación de datos y metadatos de orígenes de datos subyacentes y para usar las características avanzadas de Business Intelligence.  
  
 Se puede usar cualquier columna para la clave principal lógica, incluido un cálculo con nombre. Cuando crea una clave principal lógica, se crea una restricción exclusiva en la vista del origen de datos y se marca como una restricción de clave principal. Cualquier otra clave principal lógica existente especificada en la tabla seleccionada se elimina.  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto o conéctese a la base de datos que contiene la vista del origen de datos en que desea establecer una clave principal lógica.  
  
2.  En el Explorador de soluciones, expanda la carpeta **Vistas del origen de datos** y, después, haga doble clic en la vista del origen de datos.  
  
     Para buscar una tabla o vista, puede usar la opción **Buscar tabla** si hace clic en el menú **Vista del origen de datos**  o hace clic con el botón derecho en una zona abierta de los paneles **Tablas** o **Diagrama** .  
  
3.  En los paneles **Tablas** o **Diagrama** , haga clic con el botón derecho en las columnas que quiera usar para definir una clave principal lógica y, después, haga clic en **Establecer clave principal lógica**.  
  
     La opción para establecer una clave principal lógica únicamente está disponible en las tablas que no tienen una clave principal.  
  
     Observe que, una vez establecida la clave, aparece un icono de llave que identifica las columnas de clave principal.  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Definir cálculos con nombre en una vista del origen de datos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
