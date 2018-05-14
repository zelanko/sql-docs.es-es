---
title: Seguridad de nivel de objeto de modelo tabular | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98caa08ef6c3dcba37043124d0263507097a4374
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="object-level-security"></a>Seguridad de nivel de objeto
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Seguridad del modelo de datos se inicia con la implementación de forma eficaz [roles](../../analysis-services/tabular-models/roles-ssas-tabular.md) y filtros de nivel de fila para definir permisos de usuario en objetos de modelo de datos y los datos. A partir de los modelos tabulares 1400, también puede definir la seguridad de nivel de objeto, que incluye seguridad de nivel de tabla y la seguridad de nivel de columna en la [objeto Roles](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md).

## <a name="table-level-security"></a>Seguridad de nivel de tabla

Con la seguridad de nivel de tabla, puede no solo restringir el acceso a datos de la tabla, pero también existe nombres de tabla confidencial, ayudando a evitar que usuarios malintencionados detectar si una tabla. 

 Seguridad de nivel de tabla está establecido en los metadatos basados en JSON en Model.bim, [Tabular Model Scripting Language (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md), o [el modelo de objeto Tabular (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md). Establecer el **metadataPermission** propiedad de la **permisos de tabla** clase en el [objeto Roles](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) a **ninguno**.

En este ejemplo, se establece la propiedad metadataPermission de la clase de permisos de tabla para la tabla Product en none:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Product",
        "metadataPermission": "none"
      }
    ]
  }
```

## <a name="column-level-security"></a>Seguridad de nivel de columna

Similar a la seguridad de nivel de tabla, con la seguridad de nivel de columna puede no solo restringir el acceso a datos de la columna, sino también los nombres de columna confidencial, ayudando a evitar que usuarios malintencionados descubran una columna.

 Seguridad de nivel de columna se establece en los metadatos basados en JSON en Model.bim, [Tabular Model Scripting Language (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md), o [el modelo de objeto Tabular (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md). Establecer el **metadataPermission** propiedad de la **columnPermissions** clase en el [objeto Roles](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) a **ninguno**.

En este ejemplo, la propiedad metadataPermission de la clase columnPermissions para la columna de la tasa de Base en la tabla Employees se establece en none:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Employee",
        "columnPermissions": [
          {
            "name": "Base Rate",
            "metadataPermission": "none"
          }
        ]
      }
    ]
  }
```

## <a name="restrictions"></a>Restricciones

*  No se puede establecer la seguridad de nivel de tabla para un modelo Si interrumpe la ejecución de una cadena de relación. Se genera un error en tiempo de diseño.
 Por ejemplo, si hay relaciones entre las tablas A y B y B y C, no puede proteger la tabla B. Si la tabla B está protegida, una consulta en la tabla A no puede tránsito las relaciones entre la tabla A y B y B y C. En este caso, se podría configurar una relación diferente entre las tablas A y B.

    ![Seguridad de nivel de tabla](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  Seguridad de nivel de fila y la seguridad de nivel de objeto no se puede combinar de roles diferentes porque podría producir un acceso no deseado a los datos protegidos. Se genera un error en tiempo de consulta para los usuarios que son miembros de una combinación de este tipo de funciones.

*  Cálculos dinámicos (medidas, KPI, DetailRows) se restringen automáticamente si hacen referencia a una tabla protegida o una columna. Aunque no hay ningún mecanismo para proteger explícitamente una medida, es posible proteger implícitamente una medida mediante la actualización de la expresión para hacer referencia a una tabla protegida o una columna.

*  Las relaciones que hacen referencia a una columna protegida trabajar siempre la tabla en la columna no está protegida.




## <a name="see-also"></a>Vea también  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Objeto Roles (TMSL)](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)  
[Tabular Model Scripting Language (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
[Modelo de objetos tabulares (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md).

  
