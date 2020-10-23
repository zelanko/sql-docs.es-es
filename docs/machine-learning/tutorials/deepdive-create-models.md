---
title: Creación de modelos de R con RevoScaleR
description: Aprenda a crear un modelo de regresión lineal para analizar los datos que ha enriquecido en un tutorial anterior.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c17b74aff83412dd7f74d3c9a9cb1fb7ec711b19
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196309"
---
# <a name="create-r-models-sql-server-and-revoscaler-tutorial"></a>Creación de modelos de R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este es el tutorial 7 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Ha enriquecido los datos de entrenamiento. En este tutorial, analizará los datos mediante un modelo de regresión. Los modelos lineales son una herramienta importante en el mundo del análisis predictivo. El paquete **RevoScaleR** incluye algoritmos de regresión que pueden subdividir la carga de trabajo y ejecutarla en paralelo.

> [!div class="checklist"]
> * Crear un modelo de regresión lineal
> * Crear un modelo de regresión logística

## <a name="create-a-linear-regression-model"></a>Crear un modelo de regresión lineal

En este paso, creará un modelo lineal simple que calcula el saldo de la tarjeta de crédito del cliente, usando como variables independientes los valores de las columnas *gender* y *creditLine*.
  
Para ello, usará la función [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod), que es compatible con contextos de proceso remoto.
  
1. Cree una variable de R para almacenar el modelo completado y llame a la función **rxLinMod**, pasando una fórmula apropiada.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. Para ver un resumen de los resultados, llame a la función **summary** de R estándar en el objeto de modelo.
  
     ```R
     summary(linModObj)
     ```

Quizás piense que es peculiar que una función de R sin formato como **summary** funcione aquí, ya que en el paso anterior estableció el contexto de cálculo en el servidor. Pero incluso cuando la función **rxLinMod** usa el contexto de cálculo remoto para crear el modelo, también devuelve un objeto que contiene el modelo en su estación de trabajo local y lo almacena en el directorio compartido.

Por tanto, puede ejecutar comandos de R estándar en el modelo como si lo hubiera creado mediante el contexto "local".

**Resultados**

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

Vamos a crear un modelo de regresión logística que indica si un cliente determinado es un riesgo de fraude. Usará la función **rxLogit** de [RevoScaleR](/machine-learning-server/r-reference/revoscaler/rxlogit), que admite el ajuste de modelos de regresión logística en contextos de proceso remoto.

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
> [Puntuación de nuevos datos](../../machine-learning/tutorials/deepdive-score-new-data.md)