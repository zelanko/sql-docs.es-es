---
title: Transformar datos con RevoScaleR rxDataStep
description: Tutorial tutorial sobre cómo transformar datos con el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c7d88137994cf5d920462cc4942eb5b632ae3d6e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344680"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>Transformación de datos mediante R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, obtendrá información sobre las funciones de **RevoScaleR** para transformar datos en varias fases del análisis.

> [!div class="checklist"]
> * Usar **rxDataStep** para crear y transformar un subconjunto de datos
> * Usar **rxImport** para transformar datos en tránsito hacia o desde un archivo XDF o una trama de datos en memoria durante la importación

Aunque no son específicas para el movimiento de datos, las funciones **rxSummary**, **rxCube**, **rxLinMod**y **rxLogit** admiten transformaciones de datos.

## <a name="use-rxdatastep-to-transform-variables"></a>Usar rxDataStep para transformar variables

La función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) procesa un fragmento de datos cada vez. Para ello, lo lee en un origen de datos y lo escribe en otro. Puede especificar las columnas que se van a transformar, las transformaciones que se van a cargar, etc.

Para que este ejemplo sea interesante, vamos a usar una función de otro paquete de R para transformar los datos. El paquete **boot** es uno de los paquetes "recomendados", lo que significa que **boot** se incluye con todas las distribuciones de R, pero no se carga automáticamente en el inicio. Por lo tanto, el paquete ya debe estar disponible [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la instancia configurada para la integración de R.

En el paquete de **arranque** , use la función **inv. función logit**, que calcula el inverso de un función logit. Es decir, la función **inv.logit** convierte una función logit a una probabilidad en la escala [0,1].

> [!TIP] 
> Otra manera de obtener predicciones en esta escala sería establecer el parámetro *type* en **response** en la llamada original a **rxPredict**.

1. Empiece creando un origen de datos que contenga los datos destinados a la `ccScoreOutput`tabla,.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Agregue otro origen de datos que contenga los datos de `ccScoreOutput2`la tabla.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    En la nueva tabla, almacene todas las variables de la `ccScoreOutput` tabla anterior, además de la variable recién creada.
  
3. Establezca el contexto de proceso en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Use la función **rxSqlServerTableExists** para comprobar si la tabla `ccScoreOutput2` de salida ya existe; y si es así, use la función **rxSqlServerDropTable** para eliminar la tabla.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. Llame a la función **rxDataStep** y especifique las transformaciones deseadas en una lista.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    Al definir las transformaciones que se aplican a cada columna, también puede especificar los paquetes de R adicionales que se necesitan para realizar las transformaciones.  Para obtener más información sobre los tipos de transformaciones que puede realizar, vea [Cómo transformar y subconjuntos de datos mediante RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform).
  
6. Llame a **rxGetVarInfo** para ver un resumen de las variables del nuevo conjunto de datos.
  
```R
rxGetVarInfo(sqlOutScoreDS2)
```

**Resultado**

```R
Var 1: ccFraudLogitScore, Type: numeric
Var 2: state, Type: character
Var 3: gender, Type: character
Var 4: cardholder, Type: character
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: ccFraudProb, Type: numeric
```

Las puntuaciones originales de la función logit se conservan, pero se ha agregado una nueva columna, *ccFraudProb*, en la que las puntuaciones de la función logit se representan como valores comprendidos entre 0 y 1.

Observe que las variables de factor se han escrito en la `ccScoreOutput2` tabla como datos de caracteres. Para usarlos como factores en análisis posteriores, use el parámetro *colInfo* para especificar los niveles.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Cargar datos en memoria mediante rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)