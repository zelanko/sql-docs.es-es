---
title: "Diferencias en las caracter&#237;sticas de R entre ediciones de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Diferencias en las caracter&#237;sticas de R entre ediciones de SQL Server
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] está disponible en las siguientes ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   **Enterprise Edition**  
    
     Incluye dos servicios de R para realizar análisis en base de datos en SQL Server 2016, así como el servidor de R (independiente) en Windows, que puede utilizarse para conectarse a una variedad de bases de datos y extraer los datos para el análisis a escala, pero que no se ejecuta en bases de datos. También incluye **DeployR**, que puede utilizarse para implementar modelos y scripts de R como un servicio Web.  

     Sin restricciones. Rendimiento optimizado y escalabilidad mediante transmisión por secuencias y la ejecución en paralelo. Suopprts análisis de grandes conjuntos de datos que no caben en la memoria disponible, mediante el uso de la **utilizar otros equipos** funciones.  
  
     Análisis de base de datos de SQL Server admite regulador de recursos de script externo para personalizar el uso de recursos de servidor.  
  
-   **Developer Edition**  

    Mismas capacidades que Enterprise Edition; Sin embargo, Developer Edition no puede utilizarse en entornos de producción.  

  
  
-   **Standard Edition**  
  
     Todas las capacidades de análisis en base de datos incluye Enterprise Edition, excepto el regulador de recursos flexible. También se limita el rendimiento y escalabilidad: los datos que se pueden procesar tienen que caben en la memoria de servidor y el procesamiento se limita a un subproceso de proceso único, incluso cuando se usa el **utilizar otros equipos** funciones.
  
-   **Ediciones Express**  
  
     Sólo Express Edition con Advanced Services proporciona servicios de R. Las limitaciones de rendimiento son similares a Standard Edition.  
  
 Para obtener más información acerca de otras características del producto, consulte [características compatibles con las ediciones de SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  

> [!NOTE]
>
> + Se incluye con todas las ediciones Microsoft R Open.
> + R el cliente de Microsoft puede trabajar con todas las ediciones.
  
## Enterprise Edition  
 Rendimiento de las soluciones de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se espera que suele ser mejor que cualquier implementación convencional de R, dado el mismo hardware, ya que se puede ejecutar R con recursos de servidor y a veces se distribuye a varios procesos utilizando la **utilizar otros equipos** funciones.  
  
 Los usuarios también pueden esperar ver diferencias considerables en rendimiento y escalabilidad para las mismas funciones de R si se ejecuta en Visual Studio Enterprise Edition. Standard Edition. Razones incluyen compatibilidad para procesamiento en paralelo, la transmisión y el aumento de subprocesos disponibles para procesamiento de trabajo de R.  
  
 Sin embargo, los que el rendimiento incluso en un hardware idéntico puede verse afectado por diversos factores fuera del código R, incluyendo la competencia las demandas de recursos del servidor, el tipo de plan de consulta que se crea, cambios de esquema, la necesidad de actualizar las estadísticas o crear un nuevo plan de consulta, la fragmentación y mucho más. Es posible que un procedimiento almacenado que contiene código de R podría ejecutar en segundos en una carga de trabajo, pero realizar minutos cuando hay otros servicios que se ejecutan.  Por lo tanto, se recomienda que supervisar varios aspectos del rendimiento del servidor, incluidas redes de contextos de proceso remoto cuando cuantificación del rendimiento del trabajo de R.  

También se recomienda que configure [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) (disponible en Enterprise Edition) para personalizar la forma en que los trabajos de R están ordenados o controlados en cargas de trabajo de una sobrecarga del servidor. Puede definir funciones de clasificador para especificar el origen del trabajo de R y dar prioridad a ciertas cargas de trabajo, limitar la cantidad de memoria utilizada por las consultas SQL y controlar el número de procesos paralelos que se utiliza en una base de la carga de trabajo.  
  
## Developer Edition  
 Developer Edition proporciona un rendimiento equivalente de Enterprise Edition; Sin embargo, no se admite el uso de Developer Edition para entornos de producción.  
  
  
## Standard Edition  
 Incluso Standard Edition debe ofrecer alguna ventaja de rendimiento en comparación con los paquetes de R estándar, dada la misma configuración de hardware.  
  
 Sin embargo, Standard Edition no admite el regulador de recursos. Utilizar el regulador de recursos es la mejor manera de personalizar los recursos del servidor para admitir cargas de trabajo de R variados como modelo de entrenamiento y de puntuación.  
  
 Standard Edition también proporciona un rendimiento limitado y escalabilidad en comparación con las ediciones Enterprise y Developer. Específicamente, todos los **utilizar otros equipos** funciones y los paquetes se incluyen con la edición estándar, pero el servicio que inicia y administra los scripts de R es limitado el número de procesos que se puede usar. Además, los datos procesados por la secuencia de comandos deben caber en memoria.  
  
  
## Express Edition con Advanced Services  
 Express Edition está sujeta a las mismas limitaciones que Standard Edition.  
  
## Vea también  
 [Características compatibles con las ediciones de SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  