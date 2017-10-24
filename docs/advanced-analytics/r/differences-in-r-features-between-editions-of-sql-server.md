---
title: "Diferencias en las características de aprendizaje de máquina entre las ediciones de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9b520b7fc7e97498f4b46a43ad991558025123a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---

# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>Diferencias en las características de aprendizaje de máquina entre las ediciones de SQL Server
 
 Soporte para el aprendizaje automático está disponible en las siguientes ediciones de SQL Server 2016 y 2017 de SQL Server:

## <a name="summary-of-differences"></a>Resumen de las diferencias

-   **Enterprise Edition**
    
     SQL Server 2017 incluye servicios de aprendizaje de máquina (en las bases de datos. SQL Server 2016 incluye servicios de R. Esta característica admite el análisis de en bases de datos en SQL Server, incluido el uso de SQL Server como un contexto de proceso.
     
     SQL Server 2017 incluye Microsoft Server de aprendizaje de máquina (independiente). SQL Server 2016 incluye Microsoft R Server (independiente). Esta característica admite la puesta en marcha del que no requiere el uso de SQL Server como un contexto de proceso de aprendizaje automático.

     No hay ninguna restricción sobre estas características en Enterprise Edition, que proporciona mejor rendimiento y escalabilidad a través de la ejecución en paralelo y transmisión por secuencias. Esta edición también maximiza el uso de plataformas compatibles para la ejecución paralela y transmisión por secuencias.
     
     Análisis de bases de datos mediante SQL Server admite regulador de recursos de scripts externos para personalizar el uso de recursos de servidor.
     
     Las ediciones más recientes de Microsoft R Server son una versión mejorada del motor de puesta en marcha que admite la implementación rápida, segura y uso compartido de soluciones en R. Para obtener más información, consulte [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package).

-   **Developer Edition**

     Las mismas capacidades que Enterprise Edition, pero Developer Edition no puede usarse en entornos de producción.  
  
-   **Standard Edition**

     ¿Todas las capacidades de análisis en bases de datos se incluyen con Enterprise Edition, excepto el regulador de recursos. También se limita el rendimiento y escalabilidad: los datos que pueden ser procesados deben caber en memoria del servidor, y el procesamiento se limita a un subproceso de proceso único, incluso cuando se usa el **RevoScaleR** funciones.
  
-   **Express y Web ediciones**
  
     Solo Express Edition con Advanced Services incluye el características de aprendizaje automático. Las limitaciones de rendimiento son similares a las de Standard Edition. Edición de Web no está diseñado para tareas como la creación de modelos de aprendizaje automático; Sin embargo, puede usar la función de PREDICCIÓN para realizar puntuaciones mediante el entrenamiento de modelos en otro lugar.

-   **Azure SQL Database**
  
     Características de aprendizaje de máquina, como R y Python secuencias de comandos no se admiten en la base de datos de SQL Azure.
     
     Para obtener más información y anuncios acerca de cuándo estará disponible, esta característica, consulte el blog de SQL Server: [Python en SQL Server 2017: mejorada de aprendizaje automático en bases de datos](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


### <a name="languages-supported-in-all-editions"></a>Idiomas admitidos en todas las ediciones

Se admiten los siguientes idiomas de aprendizaje de máquina para todas las ediciones:

+ SQL Server de 2017: R y Python
+ SQL Server 2016: R solo

Microsoft R Open se incluye con todas las ediciones.

Microsoft R Open puede funcionar con todas las ediciones.

## <a name="machine-learning-in-enterprise-edition"></a>Aprendizaje en Enterprise Edition automático

Rendimiento de las soluciones de aprendizaje de máquina en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se espera suelen superar las implementaciones utilizando R convencional, dado el mismo hardware. Que se debe a que, en SQL Server, se pueden ejecutar soluciones en R con recursos de servidor y a veces se distribuye a varios procesos utilizando la **RevoScaleR** funciones. 

No se han evaluado de rendimiento para las soluciones de Python, tal y como la característica está aún en desarrollo, pero algunas de las mismas ventajas que se esperan que se aplican.

Los usuarios también pueden esperar ver diferencias considerables en rendimiento y escalabilidad para el mismo equipo, solución de aprendizaje, si se ejecutan en vs Enterprise Edition. Standard Edition. Razones incluyen compatibilidad con paralela más subprocesos disponibles para el aprendizaje automático, y procesamiento y transmisión por secuencias (o fragmentación), que permite a las funciones de RevoScaleR controlar más datos que caben en la memoria. 

Sin embargo, el rendimiento incluso en un hardware idéntico puede verse afectado por diversos factores fuera del código R o Python. Estos factores incluyen competencia demanda de recursos de servidor, el tipo de plan de consulta que se crea, cambios de esquema, la necesidad de actualizar las estadísticas o crear un nuevo plan de consulta, la fragmentación y mucho más. Es posible que un procedimiento almacenado que contiene código de R o Python podría ejecutar en segundos en una carga de trabajo, pero realizar minutos si hay otros servicios que se ejecutan.  Por lo tanto, se recomienda que supervisar varios aspectos de rendimiento del servidor, incluidas las redes de contextos de proceso remoto, al medir el rendimiento de aprendizaje de máquina.

También se recomienda que configure [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) (disponible en Enterprise Edition) para personalizar la forma en que los trabajos de script externo son un nivel de prioridad o se realiza en las cargas de trabajo de una sobrecarga del servidor. Puede definir funciones de clasificador para especificar el origen del trabajo de script externo y dar prioridad a ciertas cargas de trabajo, limitar la cantidad de memoria utilizada por las consultas SQL y controlar el número de procesos paralelos que se usan según una carga de trabajo.

## <a name="machine-learning-in-developer-edition"></a>Aprendizaje en Developer Edition automático

Developer Edition proporciona un rendimiento equivalente al de Enterprise Edition, pero no se admite el uso de Developer Edition para entornos de producción.

## <a name="machine-learning-in-standard-edition"></a>Aprendizaje en Standard Edition automático

Incluso Standard Edition debería ofrecer alguna ventaja de rendimiento en comparación con los paquetes de R estándar, dada la misma configuración de hardware.

Edición Standard no admite el regulador de recursos. Usar el regulador de recursos es la mejor manera de personalizar los recursos del servidor para admitir distintas cargas de trabajo como modelo de entrenamiento y de puntuación.

Standard Edition también proporciona rendimiento y escalabilidad limitados en comparación con las ediciones Enterprise y Developer. Todos los **RevoScaleR** funciones y los paquetes se incluyen con Standard Edition, pero el servicio que inicia y administra los scripts de R está limitado en el número de procesos que puede usar. Además, los datos procesados por el script deben caber en la memoria.  Las mismas restricciones aplican a las soluciones que usan **revoscalepy**.

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>Máquina de aprendizaje Express Edition con Advanced Services

Express Edition está sujeta a las mismas limitaciones que Standard Edition.

## <a name="machine-learning-in-web-edition"></a>Aprendizaje en las ediciones Web automático

Edición de Web no admite la ejecución de scripts de R o Python. Sin embargo, puede utilizar la función de PREDICCIÓN para realizar [puntuación nativo](../sql-native-scoring.md) en un modelo que se ha entrenado en una instancia diferente de SQL Server o servidor de R y, a continuación, se guarda en el formato binario requerido.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, vea:

+ [Ediciones y componentes de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Ediciones y componentes de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)

Para obtener más información sobre otras características de SQL Server, vea:

+ [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) 

Para obtener más información sobre las características de Microsoft R y cómo puede optimizar la solución para grandes conjuntos de datos, vea el [Microsoft R Server](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips) documentación.

