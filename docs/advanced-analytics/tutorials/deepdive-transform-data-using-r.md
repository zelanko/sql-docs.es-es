---
title: Transformar datos con R (SQL y R profundización) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80472b3328c392d886733aad97adf1aa6eeae4ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204628"
---
# <a name="transform-data-using-r-sql-and-r-deep-dive"></a>Transformar datos con R (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

El paquete **RevoScaleR** proporciona varias funciones para transformar los datos en distintas fases del análisis:

- **rxDataStep** puede usarse para crear y transformar subconjuntos de datos.

- **rxImport** admite la transformación de los datos a medida que se importan a o desde un archivo XDF o una trama de datos en memoria.

- Aunque no son específicas para el movimiento de datos, las funciones **rxSummary**, **rxCube**, **rxLinMod**y **rxLogit** admiten transformaciones de datos.

En esta sección, aprenderá a usar estas funciones. Comenzaremos con [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep).

## <a name="use-rxdatastep-to-transform-variables"></a>Utilizar rxDataStep para transformar las variables

La función **rxDataStep** procesa un fragmento de datos cada vez. Para ello, lo lee en un origen de datos y lo escribe en otro. Puede especificar las columnas que se van a transformar, las transformaciones que se van a cargar, etc.

Para hacer interesante en este ejemplo, vamos a usar una función de otro paquete de R para transformar los datos.  El paquete **boot** es uno de los paquetes "recomendados", lo que significa que **boot** se incluye con todas las distribuciones de R, pero no se carga automáticamente en el inicio. Por lo tanto, el paquete ya debe de estar disponible en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha usado con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Desde el **arranque** del paquete, utilice la función `inv.logit`, que calcula el inverso de un logit. Es decir, la función `inv.logit` convierte una función logit a una probabilidad en la escala [0,1].

> [!TIP] 
> Otra manera de obtener predicciones de esta escala sería establecer la *tipo* parámetro **respuesta** en la llamada original a rxPredict.

1. Empiece por crear un origen de datos para almacenar los datos destinados a la tabla, `ccScoreOutput`.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Agregar otro origen de datos para almacenar los datos de la tabla `ccScoreOutput2`.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    En la nueva tabla, almacenar todas las variables de la anterior `ccScoreOutput` tabla, así como la variable creada recientemente.
  
3. Establezca el contexto de proceso en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Use la función **rxSqlServerTableExists** para comprobar si la tabla de salida `ccScoreOutput2` ya existe; y si es así, use la función **rxSqlServerDropTable** para eliminar la tabla.
  
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

    Al definir las transformaciones que se aplican a cada columna, también puede especificar los paquetes de R adicionales que se necesitan para realizar las transformaciones.  Para obtener más información acerca de los tipos de transformaciones que puede realizar, vea [cómo transformar y el subconjunto de los datos con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform).
  
6. Llame a **rxGetVarInfo** para ver un resumen de las variables del nuevo conjunto de datos.
  
    ```R
    rxGetVarInfo(sqlOutScoreDS2)
    ```

    **Resultado**
    
    *Var 1: ccFraudLogitScore, Type: numeric*
    
    *Var 2: state, Type: character*
    
    *Var 3: gender, Type: character*
    
    *Var 4: cardholder, Type: character*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: ccFraudProb, Type: numeric*

Las puntuaciones originales de la función logit se conservan, pero se ha agregado una nueva columna, *ccFraudProb*, en la que las puntuaciones de la función logit se representan como valores comprendidos entre 0 y 1.

Tenga en cuenta que las variables de factor se han escrito en la tabla `ccScoreOutput2` como datos de caracteres. Para usarlos como factores en análisis posteriores, use el parámetro *colInfo* para especificar los niveles.

## <a name="next-step"></a>Paso siguiente

[Cargar datos en memoria mediante rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>Paso anterior

[Crear y ejecutar scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
