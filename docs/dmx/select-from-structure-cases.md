---
title: SELECT FROM &lt;estructura&gt;. CASOS | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 65ab4d5ebf1fbe64d3e85854df186d9ebe098e84
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600065"
---
# <a name="select-from-ltstructuregtcases"></a>SELECT FROM &lt;estructura&gt;. CASOS
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve los casos que se utilizaron para crear la estructura de minería de datos.  
  
 Si la obtención de detalles no está habilitada en la estructura, se produce un error en la instrucción. También se producirá un error en la instrucción si el usuario no tiene permisos de obtención de detalles en la estructura de minería de datos.  
  
 En [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], obtención de detalles en estructuras de minería de datos nuevas está habilitada de forma predeterminada. Para comprobar si está habilitada la obtención de detalles para una estructura determinada, compruebe si el valor de la **CacheMode** propiedad está establecida en **KeepTrainingCases**.  
  
 Si el valor de **CacheMode** cambia a **ClearAfterProcessing**, los casos de estructura se borran de la memoria caché y no se puede usar la obtención de detalles.  
  
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
  
 *expresión de condición*  
 Condición para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 Si la obtención de detalles está habilitada en la estructura y en el modelo de minería de datos, cualquier usuario que sea miembro de un rol que tenga los permisos de obtención de detalles en la estructura y en el modelo de minería de datos podrá devolver columnas de la estructura que no se incluyeron en el modelo, mediante la sintaxis siguiente:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Por lo tanto, para proteger datos confidenciales o información personal, debería crear la vista del origen de datos para enmascarar los datos personales y conceder **AllowDrillthrough** permiso en una estructura de minería de datos o modelo de minería de datos solo cuando es necesario.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes se basan en la estructura de minería de datos Targeted Mailing, que se basa en el [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] base de datos y los modelos de minería de datos asociados. Para obtener más información, consulte [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
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
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
