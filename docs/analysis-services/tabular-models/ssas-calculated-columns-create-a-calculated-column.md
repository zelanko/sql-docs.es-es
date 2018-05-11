---
title: Crear una columna calculada | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb9dd27426673409eaffeee20b648effadd0e53c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-calculated-column"></a>Crear una columna calculada
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Las columnas calculadas permiten agregar nuevos datos al modelo. En lugar de pegar o importar los valores en la columna, se crea una fórmula DAX que define los valores de nivel de fila de la columna. Los valores de cada fila de una columna calculada se calculan y se rellenan al crear una fórmula válida y hacer clic en ENTRAR. A continuación, la columna calculada se puede agregar a una aplicación de informes o de análisis como cualquier otra columna de datos. En este artículo se describe cómo crear una nueva columna calculada mediante la barra de fórmulas de DAX en el Diseñador de modelos.  
  
#### <a name="to-create-a-new-calculated-column"></a>Para crear una nueva columna calculada  
  
1.  En el diseñador de modelos, en Vista de datos, seleccione la tabla a la que desea agregar una columna calculada, haga clic en el menú **Columna** y, a continuación, haga clic en **Agregar columna**.  
  
     **Agregar columna** se resalta sobre la columna vacía situada a la derecha y el cursor se mueve a la barra de fórmulas.  
  
     Para crear una columna entre dos columnas existentes, haga clic con el botón derecho en una columna existente y, después, haga clic en **Insertar columna**.  
  
2.  En la barra de fórmulas, realice una de las siguientes acciones:  
  
    -   Escriba un signo igual seguido de una fórmula.  
  
    -   Escriba un signo igual seguido de una función DAX y, a continuación, especifique los argumentos y los parámetros que requiere la función.  
  
    -   Haga clic en el botón de función (**fx**), seleccione una categoría y una función en el cuadro de diálogo **Insertar función** y, después, haga clic en **Aceptar**. En la barra de fórmulas, escriba los argumentos y los parámetros restantes que requiere la función.  
  
3.  Presione ENTRAR para aceptar la fórmula.  
  
     Toda la columna se rellena con la fórmula y se calcula un valor para cada fila.  
  
> [!TIP]  
>  Puede usar la función Autocompletar fórmula de DAX en medio de una fórmula existente con funciones anidadas. El texto situado inmediatamente antes del punto de inserción se usa para mostrar los valores de la lista desplegable, mientras que todo el texto situado después del punto de inserción se mantiene inalterado.  
  
## <a name="see-also"></a>Vea también  
 [Columnas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  
