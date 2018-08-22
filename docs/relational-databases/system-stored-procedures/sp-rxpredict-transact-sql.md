---
title: sp_rxPredict | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
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
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f46403afef0e2f6cf967561a8fd24ec6409fe93
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2018
ms.locfileid: "40434865"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Genera un valor de predicción para una entrada determinada en función de un modelo de machine learning almacenado en un formato binario en una base de datos de SQL Server.

Proporciona la puntuación en R y Python modelos de machine learning en casi en tiempo real. `sp_rxPredict` es un procedimiento almacenado que se proporciona como un contenedor para el `rxPredict` función de R en [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) y [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)y el [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) función de Python en [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Está escrito en C++ / y está optimizado específicamente para las operaciones de puntuación.

**En este artículo se aplica a**:  
- SQL Server 2017  
- SQL Server 2016 R Services con [actualizar componentes de R](https://docs.microsoft.com/sql/advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server)

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
 
- SQL Server 2017 Machine Learning Services (incluye R Server 9.2)  
- Machine Learning Server (independiente) de SQL Server 2017 
- SQL Server R Services 2016, con una actualización de la instancia de servicios de R para R Server 9.1.0 o posterior  

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

  Para obtener información acerca de los correspondientes tipos SQL, vea [asignación de tipos de CLR de SQL](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [asignación de datos de parámetros CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

