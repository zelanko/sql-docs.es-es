---
title: sp_rxPredict | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: ede8232f36f42cc2b9758bdee8f50457ebd58dfe
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036053"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Genera un valor de predicción según un modelo almacenado.

Proporciona la puntuación en los modelos de aprendizaje automático en casi en tiempo real. `sp_rxPredict` es un procedimiento almacenado que se proporciona como un contenedor para el `rxPredict` funcionando en [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) y [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package). Está escrito en C++ / y está optimizado específicamente para las operaciones de puntuación. Admite ambos R o Python modelos de aprendizaje automático.

**En este tema se aplica a**:  
- SQL Server 2017  
- SQL Server 2016 R Services con la actualización a Microsoft R Server  

## <a name="syntax"></a>Sintaxis

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argumentos

**model**

Un modelo previamente entrenado en un formato compatible. 

**input**

Una consulta SQL válida

### <a name="return-values"></a>Valores devueltos

Se devuelve una columna de puntuación, así como las columnas de paso a través del origen de datos de entrada.
Adicionales calificación columnas, como el intervalo de confianza, puede devolverse si el algoritmo admite la generación de estos valores.

## <a name="remarks"></a>Notas

Para habilitar el uso del procedimiento almacenado, SQLCLR debe habilitarse en la instancia.

> [!NOTE]
> Antes de habilitar esta opción, tenga en cuenta las implicaciones de seguridad.

El usuario debe `EXECUTE` permiso en la base de datos.

### <a name="supported-platforms"></a>Plataformas compatibles

Requiere una de las siguientes ediciones:  
- SQL Server 2017 Machine Learning Services (incluye Microsoft R Server 9.1.0)  
- Servidor de Microsoft Machine Learning  
- SQL Server R Services 2016, con una actualización de la instancia de R Services para Microsoft R Server 9.1.0 o posterior  

### <a name="supported-algorithms"></a>Algoritmos admitidos

Para obtener una lista de algoritmos admitidos, consulte [puntuar en tiempo real](../../advanced-analytics/real-time-scoring.md).

Los siguientes tipos de modelo son **no** admite:  
- Modelos que contienen otros tipos de transformaciones de R no admitidos  
- Los modelos utilizando la `rxGlm` o `rxNaiveBayes` algoritmos de RevoScaleR  
- Modelos PMML  
- Modelos creados mediante otras bibliotecas de R de CRAN u otros repositorios  
- Modelos que contienen cualquier otro tipo de transformación de R que no aparecen aquí  

## <a name="examples"></a>Ejemplos

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

Además de ser una consulta SQL válida, los datos de entrada en *@inputData* debe incluir columnas compatibles con las columnas en el modelo almacenado.

`sp_rxPredict` admite solo los siguientes tipos de columna. NET: double, float, short, ushort, long, ulong y cadena. Es posible que deba filtrar los tipos no compatibles en los datos de entrada antes de usarlo para puntuar en tiempo real. 

  Para obtener información acerca de los correspondientes tipos SQL, vea [asignación de tipos de CLR de SQL](https://msdn.microsoft.com/library/bb386947.aspx) o [asignación de datos de parámetros CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

