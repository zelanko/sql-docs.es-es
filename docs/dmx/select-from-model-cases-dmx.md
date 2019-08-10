---
title: Seleccione del &lt;modelo&gt;. CASOS (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5f0334c37eeedafee7066f01d61745fcb82d1629
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892842"
---
# <a name="select-from-ltmodelgtcases-dmx"></a>Seleccione del &lt;modelo&gt;. CASOS (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Admite la obtención de detalles y devuelve los casos que se emplearon para el aprendizaje del modelo. También puede devolver columnas de la estructura que no están incluidas en el modelo, si la obtención de detalles se ha habilitado en la estructura de minería de datos y en el modelo de minería de datos, y si se tienen los permisos adecuados.  
  
 Si la obtención de detalles no está habilitada en el modelo de minería de datos, se produce un error de la instrucción.  
  
> [!NOTE]  
>  En Extensiones de minería de datos (DMX), solo se puede habilitar la obtención de detalles al crear el modelo de minería de datos. Puede agregar la obtención de detalles a un modelo existente utilizando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], pero se debe volver a procesar el modelo antes de poder ver o consultar los casos.  
  
 Para obtener más información sobre cómo habilitar la obtención de detalles, vea [ &#40;crear&#41;modelo de minería de datos DMX](../dmx/create-mining-model-dmx.md), [seleccionar en &#40;&#41;DMX](../dmx/select-into-dmx.md)y modificar la estructura [ &#40;de minería de datos DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Entero que especifica el número de filas que se devuelven.  
  
 *lista de expresiones*  
 Lista de expresiones separadas por comas. Una expresión puede incluir identificadores de columna, funciones definidas por el usuario, UDFs y funciones VBA, y otros elementos.  
  
 Para incluir una columna de estructura que no está incluida en el modelo de minería de datos, utilice la función `StructureColumn('<structure column name>')`.  
  
 *model*  
 Identificador de modelo.  
  
 *expresión de condición*  
 Condición para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 Si la obtención de detalles está habilitada en la estructura y en el modelo de minería de datos, los usuarios que sean miembros de un rol que tenga los permisos de obtención de detalles en la estructura y en el modelo podrán tener acceso a las columnas de la estructura de minería de datos que no están incluidas en el modelo de minería de datos. Por lo tanto, para proteger datos confidenciales o información personal, debe construir la vista del origen de datos para enmascarar información personal y conceder el permiso **AllowDrillthrough** en una estructura de minería de datos solo cuando sea necesario.  
  
 La [función &#40;lag&#41; DMX](../dmx/lag-dmx.md) se puede usar con los modelos de serie temporal para devolver o filtrar en el intervalo de tiempo entre cada caso y la hora inicial.  
  
 El uso de la función [ &#40;&#41; DMX IsInNode](../dmx/isinnode-dmx.md) en la cláusula **Where** solo devuelve los casos que están asociados al nodo especificado por la columna NODE_UNIQUE_NAME del conjunto de filas de esquema.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes se basan en la estructura de minería de datos Targeted mailing, que se [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]basa en la base de datos y sus modelos de minería de datos asociados. Para obtener más información, vea [tutorial básico de minería de datos](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>Ejemplo 1: Obtención de detalles de los casos del modelo y las columnas de estructura  
 En el siguiente ejemplo se devuelven las columnas para todos los casos que se emplearon para probar el modelo Targeted Mailing. Si la estructura de minería de datos en la que se genera el modelo no tiene un conjunto de datos de prueba de exclusión, esta consulta devolvería 0 casos. Puede utilizar la lista de expresiones para devolver únicamente las columnas que necesite.  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>Ejemplo 2: Obtención de detalles de los casos de entrenamiento en un nodo específico  
 En el ejemplo siguiente solo se devuelven los casos que se utilizaron para el aprendizaje de Clúster 2. El nodo para Clúster 2 tiene el valor 002' para la columna NODE_UNIQUE_NAME. El ejemplo también devuelve una columna de estructura, [Customer Key], que no formaba parte del modelo de minería de datos y proporciona el alias `CustomerID` para la columna. Observe que el nombre de la columna de estructura se pasa como un valor de cadena y por ello debe estar entre comillas, no entre corchetes.  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 Para devolver una columna de estructura, los permisos de obtención de detalles deben estar habilitados en el modelo de minería de datos y en la estructura de minería de datos.  
  
> [!NOTE]  
>  No todos los tipos de modelos de minería de datos admiten la obtención de detalles. Para obtener información acerca de los modelos que admiten la obtención de detalles, vea [minería &#40;&#41;de datos de consultas de obtención de detalles](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining).  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Instrucciones de definición &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-definition.md)   
 [Instrucciones de manipulación &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
