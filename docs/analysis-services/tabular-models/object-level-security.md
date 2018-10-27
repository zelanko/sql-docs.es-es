---
title: Seguridad de nivel de objeto de modelo tabular | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54384e050f4e45ad5d89d66111ecdcc851076d76
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148210"
---
# <a name="object-level-security"></a>Seguridad de nivel de objeto
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Seguridad del modelo de datos se inicia con la implementación de forma eficaz [roles](../../analysis-services/tabular-models/roles-ssas-tabular.md) y los filtros de fila para definir permisos de usuario en objetos del modelo de datos y los datos. A partir de modelos tabulares 1400, también puede definir la seguridad de nivel de objeto, que incluye seguridad de nivel de tabla y la seguridad de nivel de columna en la [objeto Roles](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl).

## <a name="table-level-security"></a>Seguridad de nivel de tabla

Con la seguridad de nivel de tabla, puede no sólo restringe el acceso a datos de la tabla, pero también existe nombres de tablas confidenciales, ayudando a evitar que usuarios malintencionados detecten si una tabla. 

 Seguridad de nivel de tabla está establecido en los metadatos basados en JSON en Model.bim, [Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference), o [el modelo de objetos tabulares (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo). Establecer el **metadataPermission** propiedad de la **permisos de tabla** clase en el [objeto Roles](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl) a **ninguno**.

En este ejemplo, la propiedad metadataPermission de la clase de permisos de tabla para la tabla Product se establece en none:

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

Similar a la seguridad de nivel de tabla, con seguridad de nivel de columna puede no sólo restringir el acceso a datos de columna, sino también los nombres de columna confidencial, ayudando a evitar que usuarios malintencionados detecten una columna.

 Seguridad de nivel de columna se establece en los metadatos basados en JSON en Model.bim, [Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference), o [el modelo de objetos tabulares (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo). Establecer el **metadataPermission** propiedad de la **permisos de columna** clase en el [objeto Roles](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl) a **ninguno**.

En este ejemplo, la propiedad metadataPermission de la clase de permisos de columna para la columna de la tasa Base en la tabla Employees se establece en none:

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

## <a name="restrictions"></a>Restrictions

*  Seguridad de nivel de tabla no se puede establecer para un modelo si divide una cadena de relación. Se genera un error en tiempo de diseño.
 Por ejemplo, si hay relaciones entre las tablas A y B y B y C, no puede proteger la tabla B. Si la tabla B está protegida, una consulta en una tabla no se permite el tránsito las relaciones entre la tabla A y B y B y C. En este caso, se podría configurar una relación independiente entre las tablas A y B.

    ![Seguridad de nivel de tabla](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  Seguridad de nivel de fila y la seguridad de nivel de objeto no pueden combinarse de roles diferentes porque el acceso no deseado podría introducir a los datos protegidos. Se genera un error en tiempo de consulta para los usuarios que son miembros de este tipo una combinación de roles.

*  Cálculos dinámicos (medidas, KPI, DetailRows) se restringen automáticamente si hacen referencia a una tabla protegida o columna. Aunque no hay ningún mecanismo para proteger de forma explícita una medida, es posible proteger implícitamente una medida mediante la actualización de la expresión para hacer referencia a una tabla protegida o columna.

*  Las relaciones que hacen referencia a una columna protegida trabajar siempre la tabla en la columna no es segura.




## <a name="see-also"></a>Vea también  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Objeto Roles (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)  
[Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)  
[Modelo de objetos tabulares (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo).

  
