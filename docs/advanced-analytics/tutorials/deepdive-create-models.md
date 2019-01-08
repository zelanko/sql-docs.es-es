---
title: Tutorial de RevoScaleR de modelos de R - de creación de SQL Server Machine Learning
description: Tutorial del tutorial sobre cómo crear un modelo usando el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 88e2dd9e50ca79136e4082cab30bba4a0e961531
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645074"
---
# <a name="create-r-models-sql-server-and-revoscaler-tutorial"></a>Crear modelos de R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Ahora que ha enriquecido los datos de entrenamiento, es momento de analizar los datos mediante el modelo de regresión. Los modelos lineales son una herramienta importante en el mundo de los análisis predictivos y el **RevoScaleR** paquete incluye algoritmos de regresión que pueden subdividir la carga de trabajo y ejecutarlo en paralelo.

> [!div class="checklist"]
> * Crear un modelo de regresión lineal
> * Crear un modelo de regresión logística

## <a name="create-a-linear-regression-model"></a>Crear un modelo de regresión lineal

En este paso, creará un modelo lineal simple que calcula el saldo de tarjeta de crédito para los clientes usando como variables independientes los valores de la *sexo* y *creditLine* columnas.
  
Para ello, use el [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) función, que es compatible con contextos de cálculo remoto.
  
1. Cree una variable de R para almacenar completado modelo y llamar a **rxLinMod**, pasando una fórmula apropiada.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. Para ver un resumen de los resultados, llame a la estándar R **resumen** función en el objeto de modelo.
  
     ```R
     summary(linModObj)
     ```

Quizás piense que es peculiar que una función de R sin formato como **summary** funcione aquí, ya que en el paso anterior estableció el contexto de cálculo en el servidor. Pero incluso cuando la función **rxLinMod** usa el contexto de cálculo remoto para crear el modelo, también devuelve un objeto que contiene el modelo en su estación de trabajo local y lo almacena en el directorio compartido.

Por tanto, puede ejecutar comandos de R estándar en el modelo como si lo hubiera creado mediante el contexto "local".

**Resultado**

```R
Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): balance
Total independent variables: 4 (Including number dropped: 1)
Number of valid observations: 10000
Number of missing observations: 0
Coefficients: (1 not defined because of singularities)

Estimate Std. Error t value Pr(>|t|) (Intercept)
3253.575 71.194 45.700 2.22e-16
gender=Male -88.813 78.360 -1.133 0.257
gender=Female Dropped Dropped Dropped Dropped
creditLine 95.379 3.862 24.694 2.22e-16
Signif. codes: 0  0.001  0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>Crear un modelo de regresión logística

A continuación, cree un modelo de regresión logística que indica si un cliente determinado es un riesgo de fraude. Deberá usar el **RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) función, contextos de cálculo que admite el ajuste de modelos de regresión logística de oficinas remotas.

Deje el contexto de cálculo como está. También seguirá usando el mismo origen de datos.

1. Llame a la función **rxLogit** y pase la fórmula necesaria para definir el modelo.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    Como es un modelo grande, que contiene 60 variables independientes, incluidas tres variables ficticias que se descartan, es posible que tenga que esperar unos minutos a que el contexto de cálculo devuelva el objeto.
    
    El motivo por el que el modelo es tan grande es que, en R (y en el paquete **RevoScaleR** ), todos los niveles de una variable de factor de categorías se tratan de forma automática como una variable ficticia independiente.
  
2. Llame a la función **summary** de R para ver un resumen del modelo devuelto.
  
    ```R
    summary(logitObj)
    ```
  
**Resultados parciales**

```R
Logistic Regression Results for: fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): fraudRisk
Total independent variables: 60 (Including number dropped: 3)
Number of valid observations: 10000 -2

LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)

Coefficients:
Estimate Std. Error z value Pr(>|z|)     (Intercept)
-8.627e+00  1.319e+00  -6.538 6.22e-11
state=AK                Dropped    Dropped Dropped  Dropped
state=AL             -1.043e+00  1.383e+00  -0.754   0.4511

(other states omitted)

gender=Male             Dropped    Dropped Dropped  Dropped
gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09
cardholder=Principal    Dropped    Dropped Dropped  Dropped
cardholder=Secondary  5.635e-01  3.403e-01   1.656   0.0977
balance               3.962e-04  1.564e-05  25.335 2.22e-16
numTrans              4.950e-02  2.202e-03  22.477 2.22e-16
numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10
creditLine            1.042e-01  4.705e-03  22.153 2.22e-16

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Puntuación de nuevos datos](../../advanced-analytics/tutorials/deepdive-score-new-data.md)