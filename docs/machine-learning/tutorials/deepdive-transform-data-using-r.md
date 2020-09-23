---
title: Transformación de datos mediante RevoScaleR
description: Obtenga información sobre las funciones de RevoScaleR para transformar datos en varias fases del análisis y cómo transformar datos con el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1d8f4419e468bfd0f82f064f59d9b3bdd1036f15
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178650"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>Transformación de datos mediante R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este es el tutorial 9 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este tutorial, obtendrá información sobre las funciones **RevoScaleR** para transformar los datos en distintas fases del análisis.

> [!div class="checklist"]
> * Usar **rxDataStep** para crear y transformar un subconjunto de datos.
> * Usar **rxImport** para transformar datos en tránsito hacia o desde un archivo XDF o una trama de datos en memoria durante la importación.

Aunque no son específicas para el movimiento de datos, las funciones **rxSummary**, **rxCube**, **rxLinMod**y **rxLogit** admiten transformaciones de datos.

## <a name="use-rxdatastep-to-transform-variables"></a>Uso de rxDataStep para transformar variables

La función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) procesa un fragmento de datos cada vez. Para ello, lo lee en un origen de datos y lo escribe en otro. Puede especificar las columnas que se van a transformar, las transformaciones que se van a cargar, etc.

Para que este ejemplo sea interesante, usaremos una función de otro paquete de R para transformar los datos. El paquete **boot** es uno de los paquetes "recomendados", lo que significa que **boot** se incluye con todas las distribuciones de R, pero no se carga automáticamente en el inicio. Por lo tanto, el paquete ya debe de estar disponible en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada para la integración de R.

Desde el paquete **boot**, use la función **inv.logit** que calcula el inverso de una función logit. Es decir, la función **inv.logit** convierte una función logit a una probabilidad en la escala [0,1].

> [!TIP] 
> Otra manera de obtener predicciones en esta escala sería establecer el parámetro *type* en **response** en la llamada original a **rxPredict**.

1. Empiece creando un origen de datos para almacenar los datos destinados a la tabla `ccScoreOutput`.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Agregue otro origen de datos para almacenar los datos para la tabla `ccScoreOutput2`.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    En la tabla nueva, almacene todas las variables de la tabla `ccScoreOutput` anterior, además de la variable recién creada.
  
3. Establezca el contexto de proceso en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Use la función **rxSqlServerTableExists** para comprobar si la tabla de salida `ccScoreOutput2` ya existe y, de ser así, use la función **rxSqlServerDropTable** para eliminar la tabla.
  
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

    Al definir las transformaciones que se aplican a cada columna, también puede especificar los paquetes de R adicionales que se necesitan para realizar las transformaciones.  Para obtener más información sobre los tipos de transformaciones que puede realizar, vea [Cómo transformar y crear un subconjunto de datos mediante RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform).
  
6. Llame a **rxGetVarInfo** para ver un resumen de las variables del nuevo conjunto de datos.
  
```R
rxGetVarInfo(sqlOutScoreDS2)
```

**Resultados**

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

Observe que las variables de factor se han escrito en la tabla `ccScoreOutput2` como datos de caracteres. Para usarlos como factores en análisis posteriores, use el parámetro *colInfo* para especificar los niveles.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Cargar datos en memoria mediante rxImport](../../machine-learning/tutorials/deepdive-load-data-into-memory-using-rximport.md)