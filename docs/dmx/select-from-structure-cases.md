---
title: SELECT FROM &lt;estructura&gt;. CASOS | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SELECT
- CASES
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- SELECT FROM <structure> statements
ms.assetid: 36f50213-14dc-42da-b899-20240b781e1a
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ea905e78ee2e1c86882981ed54defca0d8ac65d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="select-from-ltstructuregtcases"></a>SELECT FROM &lt;estructura&gt;. CASOS
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve los casos que se utilizaron para crear la estructura de minería de datos.  
  
 Si la obtención de detalles no está habilitada en la estructura, se produce un error en la instrucción. También se producirá un error en la instrucción si el usuario no tiene permisos de obtención de detalles en la estructura de minería de datos.  
  
 En [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], obtención de detalles en nuevas estructuras de minería de datos está habilitada de forma predeterminada. Para comprobar si la obtención de detalles está habilitada para una estructura determinada, compruebe si el valor de la **CacheMode** propiedad está establecida en **KeepTrainingCases**.  
  
 Si el valor de **CacheMode** se cambia a **ClearAfterProcessing**, los casos de estructura se borran de la memoria caché y no se puede utilizar la obtención de detalles.  
  
> [!NOTE]  
>  No puede habilitar o deshabilitar la obtención de detalles en la estructura de minería de datos utilizando Extensiones de minería de datos (DMX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT [TOP n] <expression list> FROM <structure>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Entero que especifica el número de filas que se devuelven.  
  
 *lista de expresiones*  
 Lista de expresiones separadas por comas.  
  
 Una expresión puede incluir identificadores de columna, funciones definidas por el usuario y funciones VBA.  
  
 *estructura*  
 Nombre de la estructura.  
  
 *Expresión de condición*  
 Condición para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 Si la obtención de detalles está habilitada en la estructura y en el modelo de minería de datos, cualquier usuario que sea miembro de un rol que tenga los permisos de obtención de detalles en la estructura y en el modelo de minería de datos podrá devolver columnas de la estructura que no se incluyeron en el modelo, mediante la sintaxis siguiente:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Por lo tanto, para proteger datos confidenciales o personales, debería crear la vista del origen de datos para enmascarar la información personal y conceder **AllowDrillthrough** permiso en una estructura de minería de datos o el modelo de minería de datos solo cuando sea necesario.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes se basan en la estructura de minería de datos Targeted Mailing, que se basa en el [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] base de datos y los modelos de minería de datos asociados. Para obtener más información, consulte [Tutorial básico de minería de datos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drill-through-to-structure-cases"></a>Ejemplo 1: obtener detalles de los casos de estructura  
 El ejemplo siguiente devuelve una lista de los 500 clientes más antiguos de la estructura de minería de datos Targeted Mailing. La consulta devuelve todas las columnas del modelo de minería de datos, pero restringe las filas a aquéllos que compraron una bicicleta y los ordena por edades. También puede editar la lista de expresiones para devolver únicamente las columnas que necesite.  
  
```  
SELECT TOP 500 *  
FROM [Targeted Mailing].Cases  
WHERE [Bike Buyer] = 1  
ORDER BY Age DESC;  
```  
  
### <a name="example-2-drillthrough-to-test-or-training-cases-only"></a>Ejemplo 2: obtener detalles únicamente de los casos de prueba o de aprendizaje  
 El ejemplo siguiente devuelve una lista de los casos de estructura de Targeted Mailing que están reservados para pruebas. Si la estructura de minería de datos no contiene un conjunto de pruebas de exclusión, de forma predeterminada todos los casos se consideran casos de aprendizaje y esta consulta devuelve 0 casos.  
  
```  
SELECT [Customer Key], Gender, Age  
FROM [Targeted Mailing].Cases  
WHERE IsTestCase();  
```  
  
 Para devolver los casos de aprendizaje, utilice la función `IsTrainingCase()`.  
  
## <a name="see-also"></a>Vea también  
 [SELECCIONE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Extensiones de minería de datos &#40;DMX&#41; las instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos & #40; DMX & #41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
