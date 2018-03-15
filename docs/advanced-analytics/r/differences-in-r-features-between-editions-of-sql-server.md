---
title: "SQL Server Machine Learning Services: disponibilidad de las características entre ediciones | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 16ca6c44b15c9fb7c1983d5a04175ebbade57895
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>Disponibilidad de las características entre ediciones de SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 Características de aprendizaje de máquina están disponibles en SQL Server 2016 y 2017 de SQL Server. Este artículo enumera las ediciones que proporciona la característica, describe las limitaciones que se aplican en ediciones específicas y enumera capacidades disponibles únicamente en determinadas ediciones.

 > [!NOTE]
 > En general, aprendizaje automático de SQL Server (In-Database) no incluye el [puesta en marcha](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) características que se incluyen en una instalación de servidor de R o servidor de aprendizaje de máquina independiente. Puesta en marcha incluye la implementación del servicio web y el hospedaje y, por tanto, compite por los mismos recursos que otras operaciones de SQL Server.
 > 
 > Por este motivo, se recomienda instalar SQL Server 2016 R Server (independiente) o el servidor de aprendizaje de SQL Server de 2017 máquina (independiente) en un servidor físico diferente para admitir la implementación de modelos de predicción como un servicio web. 

## <a name="sql-server-2017-machine-learning-services-in-database-and-standalone"></a>SQL Server de 2017 Machine Learning Services (en bases de datos) y (independiente)

La edición Developer proporciona un rendimiento equivalente a la de Enterprise Edition. No se admite el uso de Developer Edition para entornos de producción.

|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express| 
|-------|----------|--------|---|------------------------------|-------|
| Intérprete de R & paquetes propietarios | Sí | Sí | No | No | no | 
| Bibliotecas de cliente y el intérprete de Python | Sí | Sí | No | No | no | 
| Fragmentación de datos <br/>(procesar grandes cantidades de datos, más allá de lo que cabe en la memoria) | Sí | No | No | No | no |
| Procesamiento de escala vertical <br/>(más de 2 procesadores) | Sí | No | No | No | no |
| Puesta en marcha | Sí | No | No | No | no |
| [PREDECIR](../../t-sql/queries/predict-transact-sql.md) (función) <br/>(realiza [puntuación nativo](../sql-native-scoring.md) en un modelo previamente entrenado, previamente guardado en el formato binario requerido) | Sí | Sí | Sí | Sí | Sí |
| Compatibilidad con clientes de R | Sí | Sí | No | No | no | 
| Microsoft R Open | Sí | Sí | No | No | no | 
| Python anaconda 3.5 | Sí | Sí | No | No | no | 

## <a name="sql-server-2016-r-services-in-database-and-r-server-standalone"></a>R Services (en bases de datos) de SQL Server 2016 y R Server (independiente)

Disponibilidad de características es igual a 2017, menos el soporte técnico de Python que no formaba parte de la versión en primer lugar 2016.

## <a name="r-feature-availability-in-azure-sql-database"></a>Disponibilidad de características de R en la base de datos de SQL Azure
  
Después de una versión de prueba inicial, R Services está **no** disponible en la base de datos de SQL Azure, pendiente de su posterior desarrollo. 

## <a name="performance-expectations-for-enterprise-edition"></a>Expectativas de rendimiento de Enterprise Edition

Rendimiento de las soluciones de aprendizaje de máquina en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se espera suelen superar las implementaciones utilizando R convencional, dado el mismo hardware. Que se debe a que, en SQL Server, se pueden ejecutar soluciones en R con recursos de servidor y a veces se distribuye a varios procesos utilizando la **RevoScaleR** funciones. 

No se han evaluado de rendimiento para las soluciones de Python, tal y como la característica está aún en desarrollo, pero algunas de las mismas ventajas que se esperan que se aplican.

Los usuarios también pueden esperar ver diferencias considerables en rendimiento y escalabilidad para el mismo equipo, solución de aprendizaje, si se ejecutan en vs Enterprise Edition. Standard Edition. Razones incluyen compatibilidad con paralela más subprocesos disponibles para el aprendizaje automático, y procesamiento y transmisión por secuencias (o fragmentación), que permite a las funciones de RevoScaleR controlar más datos que caben en la memoria. 

Sin embargo, el rendimiento incluso en un hardware idéntico puede verse afectado por diversos factores fuera del código R o Python. Estos factores incluyen competencia demanda de recursos de servidor, el tipo de plan de consulta que se crea, cambios de esquema, la necesidad de actualizar las estadísticas o crear un nuevo plan de consulta, la fragmentación y mucho más. Es posible que un procedimiento almacenado que contiene código de R o Python podría ejecutar en segundos en una carga de trabajo, pero realizar minutos si hay otros servicios que se ejecutan.  Por lo tanto, se recomienda que supervisar varios aspectos de rendimiento del servidor, incluidas las redes de contextos de proceso remoto, al medir el rendimiento de aprendizaje de máquina.

También se recomienda que configure [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) (disponible en Enterprise Edition) para personalizar la forma en que los trabajos de script externo son un nivel de prioridad o se realiza en las cargas de trabajo de una sobrecarga del servidor. Puede definir funciones de clasificador para especificar el origen del trabajo de script externo y dar prioridad a ciertas cargas de trabajo, limitar la cantidad de memoria utilizada por las consultas SQL y controlar el número de procesos paralelos que se usan según una carga de trabajo.

## <a name="see-also"></a>Vea también

+ [Ediciones y componentes de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Ediciones y componentes de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [Sugerencias sobre cómo calcular con grandes cantidades de datos en R (servidor de aprendizaje de máquina)](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
