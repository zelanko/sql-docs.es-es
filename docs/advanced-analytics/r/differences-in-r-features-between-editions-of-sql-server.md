---
title: 'SQL Server Machine Learning Services: disponibilidad de las características entre ediciones | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/17/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ''
caps.latest.revision: ''
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 50c9f2c8f1039ce0bba25ed9c6b7c5564c1d10d2
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>Disponibilidad de las características entre ediciones de SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 Características de aprendizaje de máquina están disponibles en SQL Server 2016 y 2017 de SQL Server. Este artículo enumera las ediciones que proporciona la característica, describe las limitaciones que se aplican en ediciones específicas y enumera capacidades disponibles únicamente en determinadas ediciones.


## <a name="sql-server-2017-features"></a>Características de SQL Server 2017

Las ediciones Enterprise y Developer tienen la misma cobertura de característica para que pueda crear soluciones para una instalación de Enterprise sin incurrir en el mismo costo. Aunque las ediciones son funcionalmente equivalentes, no se admite el uso de la edición Developer para entornos de producción.

La diferencia entre la integración básica y avanzada es la escala. Integración avanzada puede usar todos los núcleos disponibles para el procesamiento paralelo de conjuntos de datos en cualquier tamaño que puede dar cabida su equipo. La integración básica se limita a 2 núcleos y conjuntos de datos de conexión en la memoria. 

Integración básica y avanzada se aplica a las instancias (en bases de datos). Un servidor independiente no es una característica de instancia de motor de base de datos y se ofrece como una opción de instalación solo en las ediciones Developer y Enterprise.

|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integración básica de R|Sí|Sí|Sí|Sí|no|   
|Integración avanzada de R|Sí|No|No|No|no| 
|Integración básica de Python|Sí|Sí|Sí|Sí|no|
|Integración avanzada de Python|Sí|No|No|No|no| 
|Machine Learning Server (independiente)|Sí|No|No|No|no|   

 > [!NOTE]
 > Sólo un servidor (independiente) ofrece la [puesta en marcha](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) características que se incluyen en una instalación (sin SQL-marca) R Server o servidor de aprendizaje de máquina de Microsoft. Puesta en marcha incluye la implementación del servicio web y las capacidades de hospedaje.
>
> Para una instalación (In-Database), el método equivalente para soluciones en marcha es al aprovechar las capacidades del motor de base de datos, al convertir un código a una función que se puede ejecutar en un procedimiento almacenado.


## <a name="sql-server-2016-r-features"></a>Características de SQL Server 2016 R

SQL Server 2016 incluye la integración de R solo. En SQL Server 2016, son equivalentes a SQL Server 2017 integración de R básica y avanzada.

## <a name="r-feature-availability-in-azure-sql-database"></a>Disponibilidad de características de R en la base de datos de SQL Azure
  
Después de una versión de prueba inicial, R Services se quitó de la base de datos de SQL Azure, pendiente de desarrollo adicional. 

## <a name="performance-expectations-for-enterprise-edition"></a>Expectativas de rendimiento de Enterprise Edition

Rendimiento de las soluciones de aprendizaje de máquina en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se espera suelen superar las implementaciones utilizando R convencional, dado el mismo hardware. Que se debe a que, en SQL Server, se pueden ejecutar soluciones en R con recursos de servidor y a veces se distribuye a varios procesos utilizando la **RevoScaleR** funciones. 

Los usuarios también pueden esperar ver diferencias considerables en rendimiento y escalabilidad para el mismo equipo, solución de aprendizaje, si se ejecutan en vs Enterprise Edition. Standard Edition. Razones incluyen compatibilidad con paralela más subprocesos disponibles para el aprendizaje automático, y procesamiento y transmisión por secuencias (o fragmentación), que permite a las funciones de RevoScaleR controlar más datos que caben en la memoria. 

Sin embargo, el rendimiento incluso en un hardware idéntico puede verse afectado por diversos factores fuera del código R o Python. Estos factores incluyen competencia demanda de recursos de servidor, el tipo de plan de consulta que se crea, cambios de esquema, la necesidad de actualizar las estadísticas o crear un nuevo plan de consulta, la fragmentación y mucho más. Es posible que un procedimiento almacenado que contiene código de R o Python podría ejecutar en segundos en una carga de trabajo, pero realizar minutos si hay otros servicios que se ejecutan.  Por lo tanto, se recomienda que supervisar varios aspectos de rendimiento del servidor, incluidas las redes de contextos de proceso remoto, al medir el rendimiento de aprendizaje de máquina.

También se recomienda que configure [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) (disponible en Enterprise Edition) para personalizar la forma en que los trabajos de script externo son un nivel de prioridad o se realiza en las cargas de trabajo de una sobrecarga del servidor. Puede definir funciones de clasificador para especificar el origen del trabajo de script externo y dar prioridad a ciertas cargas de trabajo, limitar la cantidad de memoria utilizada por las consultas SQL y controlar el número de procesos paralelos que se usan según una carga de trabajo.

## <a name="see-also"></a>Vea también

+ [Ediciones y componentes de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Ediciones y componentes de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [Sugerencias sobre cómo calcular con grandes cantidades de datos en R (servidor de aprendizaje de máquina)](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
