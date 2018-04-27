---
title: ¿Qué es SQL Server Machine Learning Services? | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1b33d7fb0736e1d87aa46d052ff9e42fa740662e
ms.sourcegitcommit: 31df356f89c4cd91ba90dac609a7eb50b13836de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2018
---
# <a name="what-is-sql-server-machine-learning-services"></a>¿Qué es SQL Server Machine Learning Services?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Servicios de aprendizaje de máquina de SQL Server es un incrustado, predicción de datos y análisis ciencia motor que puede ejecutar código R y Python dentro de una base de datos de SQL Server como procedimientos almacenados, como script T-SQL que contiene instrucciones de R o Python o como contenedor de código de R o Python INSTRUCCIÓN T-SQL. 

La propuesta de valor de clave de servicios de aprendizaje de máquina es la potencia de sus paquetes propietarios para ofrecer análisis avanzados en escala y la capacidad para mostrar cálculos y procesamiento de donde residen los datos, lo que elimina la necesidad de extraer los datos a través de la red.

Hay dos opciones para usar las capacidades de aprendizaje de máquina en SQL Server: 

+ [**Servicios de aprendizaje de máquina (en bases de datos) de SQL Server** ](r/sql-server-r-services.md) funciona dentro de la instancia del motor de base de datos, donde el motor de cálculo está totalmente integrado con el motor de base de datos. La mayoría de las instalaciones son esta opción.
+ [**Aprendizaje de máquina SQL Server (independiente)** ](r/r-server-standalone.md) es una instalación de SQL no. Aunque utilice el programa de instalación de SQL Server para instalar al servidor, se separa por completo de SQL Server. Funcionalmente, equivale a la no son de SQL [Server para Windows de Microsoft Machine Learning](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

## <a name="r-and-python-packages"></a>Paquetes de R y Python

Soporte para cada idioma es a través de la propiedad paquetes de Microsoft usados para crear y entrenar modelos de distintos tipos de datos y procesamiento en paralelo con los recursos del sistema subyacente de puntuación.

Como los paquetes propietarios se basan en distribuciones de código abierto R y Python, un script o código que se ejecutan en SQL Server también puede llamar a funciones de base y usar paquetes de terceros compatibles con la versión de idioma incluida en SQL Server (3.5 de Python y versiones recientes de R, 3.3.3 actualmente).

| L  | Python | Description |
|-----------|----------------|-------------|
| [RevoScaleR](r/revoscaler-overview.md) | [revoscalepy](python/what-is-revoscalepy.md)   | Las funciones de estas bibliotecas se encuentran entre las más usadas. Transformaciones de datos y manipulación, resumen estadístico, visualización y muchos tipos de modelado y análisis se encuentran en estas bibliotecas. Además, las funciones de estas bibliotecas distribuyen automáticamente las cargas de trabajo a través de núcleos disponibles para el procesamiento en paralelo, con la posibilidad de trabajar con los fragmentos de datos que se coordina y administra el motor de cálculo. |
| [MicrosoftML](using-the-microsoftml-package.md) | [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Algoritmos de características de la imagen, problemas de clasificación y mucho más de aprendizaje automático de líderes en la industria. |
| [OlapR](r/how-to-create-mdx-queries-using-olapr.md) | none | Compilar o ejecutar una consulta MDX en un script de R.
| [SqlRUtils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) | none | Funciones para colocar scripts de R en un instrucción T-SQL procedimiento almacenan, registrar un procedimiento almacenado con una base de datos y ejecutar el procedimiento almacenado desde un entorno de desarrollo de R.
| [mrsdeploy](operationalization-with-mrsdeploy.md) | none | Utiliza principalmente en una instalación de no son de SQL del servidor de aprendizaje de máquina, como el [(independiente) versión](r/r-server-standalone.md). Usar este paquete para implementar y alojar servicios web, topologías de escalabilidad horizontal con web dedicado de compilación y nodos de proceso, alternar entre sesiones locales como remotas, ejecutar diagnósticos y mucho más. Para una instalación (In-Database), use este paquete con una capacidad de cliente: por ejemplo tener acceso a un servicio web en un servidor remoto dedicado a ejecutar solo cargas de trabajo de servicios de aprendizaje de máquina. |

Portabilidad del código R y Python personalizado se dirige a través de la distribución de paquetes e intérpretes que están integrados en varios productos. Los mismos paquetes que se incluyen en SQL Server también están disponibles en varios otros productos y servicios, incluidas las versiones no son de SQL denominada [aprendizaje de máquina de Microsoft Server](https://docs.microsoft.com/machine-learning-server/). Los clientes gratuitos que incluyen nuestro intérpretes de R y Python incluyen [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) y [bibliotecas de Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

También están disponibles en varios paquetes e intérpretes [máquinas virtuales de Azure](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux), aprendizaje automático de Azure y servicios de Azure como [HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight). 


## <a name="use-cases"></a>Casos de uso

**Análisis de bases de datos**

Los programadores y analistas suelen tengan el código que se ejecuta sobre una instancia de SQL Server local. Si tiene SQL Server y un IDE como [Visual Studio con R](https://docs.microsoft.com/visualstudio/rtvs/) o [Visual Studio con Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio) en el mismo equipo, puede crear, entrenar y probar modelos localmente en cualquier lenguaje. Acceso local simplifica la administración de paquetes: como administrador, puede cargar paquetes adicionales de terceros mediante permisos integrados para ese rol.

El enfoque más común para el análisis en bases de datos consiste en usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para ejecutar script de R o Python. Los tutoriales enumerados en [pasos siguientes](#next-steps) para empezar.

**Configuraciones de cliente / servidor**

Desde cualquier estación de trabajo cliente que tenga un IDE, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) o [bibliotecas de Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)y, a continuación, escribir código que inserta la ejecución (denominados un *contexto de proceso remoto*) para los datos y las operaciones a un servidor SQL remoto. 

De forma similar, si está utilizando la edición Developer, puede crear soluciones en una estación de trabajo de cliente utilizando las mismas bibliotecas e intérpretes y, a continuación, implementar código de producción en servicios de aprendizaje de máquina (en bases de datos) de SQL Server. 

## <a name="version-history"></a>Historial de versiones

Servicios de aprendizaje de SQL Server de 2017 máquina es la siguiente generación de SQL Server 2016 R Services, que se ha mejorado para incluir Python. En la tabla siguiente es una lista completa de todas las versiones, desde el comienzo a la versión actual. 

| Nombre del producto | Versión del motor | Fecha de lanzamiento |
|--------------|---------|--------------|
| Servicios de aprendizaje de máquina (en bases de datos) de SQL Server de 2017 | R Server 9.2.1 <br/> Servidor de Python 9.2 | Octubre de 2017 |
| Servidor de aprendizaje de SQL Server de 2017 máquina (independiente) | R Server 9.2.1 <br/> Servidor de Python 9.2 | Octubre de 2017 |
| SQL Server 2016 R Services (In-Database) | R Server 9.1  | Julio de 2017  |
| SQL Server 2016 R Server (independiente)  |  R Server 9.1 | Julio de 2017 |



## <a name="documentation-for-each-version"></a>Documentación de cada versión

Las versiones recientes de documentación de SQL Server son independientes de la versión. Para servicios de aprendizaje de máquina de SQL Server, Python solo está disponible en 2017 y versiones posteriores, mientras la compatibilidad de R se encuentra en todas las versiones. A menos que se indique lo contrario, puede asumir la documentación de R se aplica a las versiones de 2016 y 2017.


## <a name="related-machine-learning-products"></a>Productos de aprendizaje de máquina relacionado

 +  [Aprovisionar una máquina Virtual de Azure](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure marketplace incluye varias imágenes de máquina virtual que incluyen un servidor de aprendizaje de máquina o servidor de R. Crear una máquina virtual en Microsoft Azure es la manera más rápida de obtener al desarrollo e implementación de modelos de predicción. Imágenes de proceden con las características de ajuste de escala y uso compartido ya configurado, lo que facilita la que se va a incrustar análisis dentro de las aplicaciones como se integra con sistemas de back-end.

+ [Data Science Virtual Machine](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)

  La versión más reciente de la máquina Virtual de ciencia de datos incluye el servidor de aprendizaje de máquina, SQL Server, y una matriz de las herramientas más populares de aprendizaje automático, todos preinstalado y probado. Crear Jupyter blocs de notas, desarrollar soluciones de Julia y usar las bibliotecas de aprendizaje profundo basadas en la GPU como MXNet, CNTK y TensorFlow.

<a name="next-steps"></a>

## <a name="next-steps"></a>Pasos siguientes

**Paso 1:** instalar y configurar el software. 

+ [Instalar servicios de aprendizaje automático SQL Server de 2017 (en bases de datos)](install/sql-machine-learning-services-windows-install.md)

**Paso 2:** empezar a trabajar con código mediante cualquiera de estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](tutorials/run-python-using-t-sql.md)
+ [Tutorial: Ejecutar R en T-SQL](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

**Paso 3:** agregar los paquetes de R y Python favoritos y usarlas junto con los paquetes suministrados por Microsoft

+ [Administración de paquetes de R para SQL Server](r/r-package-management-for-sql-server-r-services.md)
