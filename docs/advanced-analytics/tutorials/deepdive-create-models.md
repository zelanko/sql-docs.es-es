---
title: Crear modelos de R | Documentos de Microsoft
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: a195d5e2-72e2-4dd6-bf43-947312e4a52a
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b5bb3c7947b3cf1cfaeea86156b3fbad9ce3535
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="create-r-models"></a>Crear modelos de R

Ahora que ha enriquecido los datos de aprendizaje, es el momento de analizarlos con la regresión lineal. Los modelos lineales son una herramienta importante en el mundo del análisis predictivo y el paquete **RevoScaleR** de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluye un algoritmo de alto rendimiento y escalable.

## <a name="create-a-linear-regression-model"></a>Crear un modelo de regresión lineal

Creará un modelo lineal simple que calcula el saldo de la tarjeta de crédito del cliente, usando como variables independientes los valores de las columnas *gender* y *creditLine* .
  
Para ello, usará la función **rxLinMod** , que es compatible con contextos de cálculo remoto.
  
1. Cree una variable de R para almacenar el modelo completado y llame a la función *rxLinMod* , pasando una fórmula apropiada.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. Para ver un resumen de los resultados, puede llamar a la función *summary* de R estándar en el objeto de modelo.
  
     ```R
     summary(linModObj)
     ```

Quizás piense que es peculiar que una función de R sin formato como **summary** funcione aquí, ya que en el paso anterior estableció el contexto de cálculo en el servidor. Pero incluso cuando la función **rxLinMod** usa el contexto de cálculo remoto para crear el modelo, también devuelve un objeto que contiene el modelo en su estación de trabajo local y lo almacena en el directorio compartido.

Por tanto, puede ejecutar comandos de R estándar en el modelo como si lo hubiera creado mediante el contexto "local".

**Resultado**

*Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)*

*Dependent variable(s): balance*

*Total independent variables: 4 (Including number dropped: 1)*

*Number of valid observations: 10000*

*Number of missing observations: 0*

*Coefficients: (1 not defined because of singularities)*

*Estimate Std. Valor de error t Pr (> | t |) (Intersección)*

*3253.575 71.194 45.700 2.22e-16*

*gender=Male -88.813 78.360 -1.133 0.257*

*gender=Female Dropped Dropped Dropped Dropped*

*creditLine 95.379 3.862 24.694 2.22e-16*

*Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1*

*Residual standard error: 3812 on 9997 degrees of freedom*

*Multiple R-squared: 0.05765*

*Adjusted R-squared: 0.05746*

*F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16*

*Condition number: 1.0184*

## <a name="create-a-logistic-regression-model"></a>Crear un modelo de regresión logística

Ahora, creará un modelo de regresión logística que indica si un cliente determinado es un riesgo de fraude. Usará la función *rxLogit* (incluida en el paquete **RevoScaleR** ), que admite el ajuste de modelos de regresión logística en contextos de cálculo remoto.

1.  Deje el contexto de cálculo como está. También seguirá usando el mismo origen de datos.

2.  Llame a la función **rxLogit** y pase la fórmula necesaria para definir el modelo.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance +      numTrans + numIntlTrans + creditLine, data = sqlFraudDS,      dropFirst = TRUE)
    ```
  
    Como es un modelo grande, que contiene 60 variables independientes, incluidas tres variables ficticias que se descartan, es posible que tenga que esperar unos minutos a que el contexto de cálculo devuelva el objeto.
    
    El motivo por el que el modelo es tan grande es que, en R (y en el paquete **RevoScaleR** ), todos los niveles de una variable de factor de categorías se tratan de forma automática como una variable ficticia independiente.
  
3.  Llame a la función **summary** de R para ver un resumen del modelo devuelto.
  
    ```R
    summary(logitObj)
    ```
  
**Resultados parciales**

*Logistic Regression Results for: fraudRisk ~ state + gender +     cardholder + balance + numTrans + numIntlTrans + creditLine*

*Data: sqlFraudDS (RxSqlServerData Data Source)*

*Dependent variable(s): fraudRisk*

*Total independent variables: 60 (Including number dropped: 3)*

*Número de observaciones válidas: 10000 -2*

*LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)*

*Coefficients:*

*Estimate Std. Error z value Pr(>|z|)     (Intercept)*

*-8.627e+00  1.319e+00  -6.538 6.22e-11*

*state=AK                Dropped    Dropped Dropped  Dropped*

*state=AL             -1.043e+00  1.383e+00  -0.754   0.4511*

*(other states omitted)*

*gender=Male             Dropped    Dropped Dropped  Dropped*

*gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09*

*cardholder=Principal    Dropped    Dropped Dropped  Dropped*

*información de los titulares = 5.635e secundaria-01 3.403e-01 1.656 0.0977*

*balance               3.962e-04  1.564e-05  25.335 2.22e-16*

*numTrans              4.950e-02  2.202e-03  22.477 2.22e-16*

*numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10*

*creditLine            1.042e-01  4.705e-03  22.153 2.22e-16*

*---*

*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*

*Condition number of final variance-covariance matrix: 3997.308*

*Number of iterations: 15*

## <a name="next-step"></a>Paso siguiente

[Nuevos datos de puntuación](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>Paso anterior

[Visualizar datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)


