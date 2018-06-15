---
title: Crear modelos de R (SQL y R profundización) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a2f6e9b23e1592073c1b21bc41e4975ffaf17075
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32446849"
---
# <a name="create-r-models-sql-and-r-deep-dive"></a>Crear modelos de R (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Ahora que ha enriquecido los datos de aprendizaje, es el momento de analizarlos con la regresión lineal. Los modelos lineales son una herramienta importante en el mundo del análisis predictivo y el paquete **RevoScaleR** de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluye un algoritmo de alto rendimiento y escalable.

## <a name="create-a-linear-regression-model"></a>Crear un modelo de regresión lineal

En este paso, creará un modelo lineal simple que calcula el saldo de tarjeta de crédito para los clientes, con lo que se usan como variables independientes los valores de la *género* y *creditLine* columnas.
  
Para ello, use la [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) función, que es compatible con contextos de proceso remoto.
  
1. Cree una variable de R para almacenar el completado modelo y llame a **rxLinMod**, pasando una fórmula apropiada.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. Para ver un resumen de los resultados, llame a la estándar R `summary` función en el objeto de modelo.
  
     ```R
     summary(linModObj)
     ```

Puede que piense peculiar que una función de R sin formato como `summary` funcionará en este caso, puesto que en el paso anterior, se establece el contexto de proceso al servidor. Pero incluso cuando la función **rxLinMod** usa el contexto de cálculo remoto para crear el modelo, también devuelve un objeto que contiene el modelo en su estación de trabajo local y lo almacena en el directorio compartido.

Por tanto, puede ejecutar comandos de R estándar en el modelo como si lo hubiera creado mediante el contexto "local".

**Resultado**

```
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
Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>Crear un modelo de regresión logística

A continuación, cree un modelo de regresión logística que indica si un cliente determinado es un riesgo de fraude. Usará el **RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) función, contextos de proceso que admite realizar el ajuste de los modelos de regresión logística en remoto.

1.  Deje el contexto de cálculo como está. También seguirá usando el mismo origen de datos.

2.  Llame a la función **rxLogit** y pase la fórmula necesaria para definir el modelo.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    Como es un modelo grande, que contiene 60 variables independientes, incluidas tres variables ficticias que se descartan, es posible que tenga que esperar unos minutos a que el contexto de cálculo devuelva el objeto.
    
    El motivo por el que el modelo es tan grande es que, en R (y en el paquete **RevoScaleR** ), todos los niveles de una variable de factor de categorías se tratan de forma automática como una variable ficticia independiente.
  
3.  Para ver un resumen del modelo devuelto, llame a la R `summary` función.
  
    ```R
    summary(logitObj)
    ```
  
**Resultados parciales**

```
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

Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-step"></a>Paso siguiente

[Nuevos datos de puntuación](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>Paso anterior

[Visualizar datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
