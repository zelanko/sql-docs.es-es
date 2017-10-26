---
title: SELECT FROM &lt;modelo&gt;. CASOS (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- CASES
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- SELECT FROM <model>.CASES statement
- drillthrough [DMX]
ms.assetid: d58acb47-aaa6-40b7-b8c4-6a6700fbc1dd
caps.latest.revision: 55
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7f5ec287b2da5998748c19a5000a0a95b658f853
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgtcases-dmx"></a>SELECT FROM &lt;modelo&gt;. CASOS (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Admite la obtención de detalles y devuelve los casos que se emplearon para el aprendizaje del modelo. También puede devolver columnas de la estructura que no están incluidas en el modelo, si la obtención de detalles se ha habilitado en la estructura de minería de datos y en el modelo de minería de datos, y si se tienen los permisos adecuados.  
  
 Si la obtención de detalles no está habilitada en el modelo de minería de datos, se produce un error de la instrucción.  
  
> [!NOTE]  
>  En Extensiones de minería de datos (DMX), solo se puede habilitar la obtención de detalles al crear el modelo de minería de datos. Puede agregar la obtención de detalles a un modelo existente utilizando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], pero se debe volver a procesar el modelo antes de poder ver o consultar los casos.  
  
 Para obtener más información acerca de cómo habilitar la obtención de detalles, vea [CREATE MINING MODEL &#40; DMX &#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md), y [ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md).  
  
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
 Si la obtención de detalles está habilitada en la estructura y en el modelo de minería de datos, los usuarios que sean miembros de un rol que tenga los permisos de obtención de detalles en la estructura y en el modelo podrán tener acceso a las columnas de la estructura de minería de datos que no están incluidas en el modelo de minería de datos. Por lo tanto, para proteger datos confidenciales o personales, debería crear la vista del origen de datos para enmascarar la información personal y conceder **AllowDrillthrough** permiso en una estructura de minería de datos solo cuando sea necesario.  
  
 El [Lag &#40; DMX &#41;](../dmx/lag-dmx.md) función puede utilizarse con modelos de serie temporal para devolver o filtrar en el intervalo de tiempo entre cada caso y la hora de inicio.  
  
 Mediante el [IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md) funcionando en el **donde** cláusula solo devuelve casos que están asociados con el nodo que se especifica mediante la columna NODE_UNIQUE_NAME del conjunto de filas de esquema.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes se basan en la estructura de minería de datos Targeted Mailing, que se basa en el [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]base de datos y sus modelos de minería de datos asociados. Para obtener más información, consulte [Tutorial básico de minería de datos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>Ejemplo 1: obtención de detalles de los casos del modelo y de las columnas de estructura  
 En el siguiente ejemplo se devuelven las columnas para todos los casos que se emplearon para probar el modelo Targeted Mailing. Si la estructura de minería de datos en la que se genera el modelo no tiene un conjunto de datos de prueba de exclusión, esta consulta devolvería 0 casos. Puede utilizar la lista de expresiones para devolver únicamente las columnas que necesite.  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>Ejemplo 2: obtención de detalles de los casos de aprendizaje en un nodo concreto  
 En el ejemplo siguiente solo se devuelven los casos que se utilizaron para el aprendizaje de Clúster 2. El nodo para Clúster 2 tiene el valor 002' para la columna NODE_UNIQUE_NAME. El ejemplo también devuelve una columna de estructura, [Customer Key], que no formaba parte del modelo de minería de datos y proporciona el alias `CustomerID` para la columna. Observe que el nombre de la columna de estructura se pasa como un valor de cadena y por ello debe estar entre comillas, no entre corchetes.  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 Para devolver una columna de estructura, los permisos de obtención de detalles deben estar habilitados en el modelo de minería de datos y en la estructura de minería de datos.  
  
> [!NOTE]  
>  No todos los tipos de modelos de minería de datos admiten la obtención de detalles. Para obtener información acerca de los modelos que admiten la obtención de detalles, vea [consultas de obtención de detalles &#40; minería de datos &#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40; DMX &#41;](../dmx/select-dmx.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

