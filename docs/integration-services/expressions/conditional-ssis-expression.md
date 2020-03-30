---
title: '? : (Condicional) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- conditional operator (?:)
- '?: (conditional operator)'
ms.assetid: d38e6890-7338-4ce0-a837-2dbb41823a37
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 758cd90c3932d59e725f6a8a9bf829e59ecf5474
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71290162"
---
# <a name="--conditional-ssis-expression"></a>? : (Condicional) (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Devuelve una de dos expresiones en función del resultado de la evaluación de una expresión booleana. Si la evaluación de la expresión booleana devuelve TRUE, se evalúa la primera expresión y el resultado es el resultado de la expresión. Si devuelve FALSE, se evalúa la segunda expresión y el resultado es el resultado de la expresión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
boolean_expression?expression1:expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 Cualquier expresión válida cuya evaluación devuelva TRUE, FALSE o NULL.  
  
 *expression1*  
 Es cualquier expresión válida.  
  
 *expression2*  
 Es cualquier expresión válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 Tipo de datos de *expression1* o *expression2*.  
  
## <a name="remarks"></a>Observaciones  
 Si el valor *boolean_expression* se evalúa como NULL, el resultado de la expresión es NULL. Si una expresión seleccionada, *expression1* o *expression2* , es NULL, el resultado es NULL. Si la expresión seleccionada no es NULL, pero la expresión no seleccionada es NULL, el resultado será el valor de la expresión seleccionada.  
  
 Si *expression1* y *expression2* tienen el mismo tipo de datos, el resultado será ese tipo de datos. Además, las reglas siguientes se aplican a los tipos de resultado:  
  
-   El tipo de datos DT_TEXT necesita que *expression1* y *expression2* tengan la misma página de código.  
  
-   La longitud de un resultado con el tipo de datos DT_BYTES es la del argumento más largo.  
  
 El conjunto de expresiones, *expression1* y *expression2*, debe tener como resultado tipos de datos válidos y seguir una de estas reglas:  
  
-   **Numeric***expression1* y *expression2* deben ser un tipo de datos numérico. La intersección de los tipos de datos debe ser un tipo de datos numérico, tal como se especifica en las reglas para las conversiones numéricas implícitas que realiza el evaluador de expresiones. La intersección de dos tipos de datos numéricos no puede ser NULL. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
-   **Cadena***expression1* y *expression2* deben tener un tipo de datos de cadena: DT_STR o DT_WSTR. Las dos expresiones pueden tener tipos de datos de cadena distintos. El resultado tiene el tipo de datos DT_WSTR con la longitud del argumento más largo.  
  
-   **Date, Time o Date/Time***expression1* y *expression2* deben devolver uno de los siguientes tipos de datos: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET o DT_FILETIME.  
  
    > [!NOTE]  
    >  El sistema no admite comparaciones entre una expresión que devuelve un tipo de datos de hora y una expresión que devuelve un tipo de datos de fecha o de fecha/hora. El sistema genera un error.  
  
     Al comparar expresiones, el sistema aplica las reglas de conversión siguientes en el orden enumerado:  
  
    -   Cuando las dos expresiones devuelven el mismo tipo de datos, se realiza una comparación de ese tipo de datos.  
  
    -   Si una expresión es un tipo de datos DT_DBTIMESTAMPOFFSET, la otra expresión se convierte en DT_DBTIMESTAMPOFFSET implícitamente y se realiza una comparación de DT_DBTIMESTAMPOFFSET. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
    -   Si una expresión es un tipo de datos DT_DBTIMESTAMP2, la otra expresión se convierte en DT_DBTIMESTAMP2 implícitamente y se realiza una comparación de DT_DBTIMESTAMP2.  
  
    -   Si una expresión es un tipo de datos DT_DBTIME2, la otra expresión se convierte en DT_DBTIME2 implícitamente y se realiza una comparación de DT_DBTIME2.  
  
    -   Si una expresión es de un tipo de datos que no es DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 o DT_DBTIME2, las expresiones se convierten en el tipo de datos DT_DBTIMESTAMP antes de compararse.  
  
     Al comparar las expresiones, el sistema hace las suposiciones siguientes:  
  
    -   Si cada expresión es un tipo de datos que incluye fracciones de segundo, el sistema supone que el tipo de datos con el menor número de dígitos por fracciones de segundo tiene ceros para los dígitos restantes.  
  
    -   Si cada expresión es un tipo de datos de fecha, pero solo una tiene un ajuste de zona horaria, el sistema supone que el tipo de datos de fecha sin ajuste de zona horaria está en hora universal coordinada (UTC).  
  
 Para obtener más información acerca de los tipos de datos, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En este ejemplo se muestra una expresión que se evalúa condicionalmente como `savannah` o `unknown`.  
  
```  
@AnimalName == "Elephant"? "savannah": "unknown"  
```  
  
 En este ejemplo se muestra una expresión que hace referencia a una columna **ListPrice** . **ListPrice** tiene el tipo de datos DT_CY. La expresión multiplica condicionalmente **ListPrice** por 0,2 o 0,1.  
  
```  
ListPrice < 350.00 ? ListPrice * .2 : ListPrice * .1  
```  
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
