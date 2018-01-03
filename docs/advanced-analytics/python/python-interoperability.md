---
title: Interoperabilidad de Python con SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5c29edc6f5b89b35e2242f9d80caf56c90426d9f
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="python-interoperability-with-sql-server"></a>Interoperabilidad de Python con SQL Server

En este tema se describe los componentes de Python que se instalan si se habilita la característica **Machine Learning Services (In-Database)** y seleccione Python como lenguaje.

## <a name="python-components"></a>Componentes de Python

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]no modifica los archivos ejecutables de Python. El tiempo de ejecución de Python se instala independientemente de las herramientas de SQL y se ejecuta fuera de la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] proceso.

La distribución que está asociada con un valor concreto [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia puede encontrarse en la carpeta asociada con la instancia.

Por ejemplo, si instala Servicios de aprendizaje de máquina con la opción de Python en la instancia predeterminada, mire debajo:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Instalación de SQL Server de 2017 Machine Learning Services agrega la distribución de Anaconda de Python. En concreto, se usan los instaladores Anaconda 3, en función de la bifurcación Anaconda 4.3. El nivel de Python esperado para SQL Server 2017 es 3.5 de Python.

## <a name="new-python-packages-in-this-release"></a>Nuevos paquetes de Python en esta versión

Para obtener una lista de paquetes admitidos por la distribución de Anaconda, vea el sitio de análisis de Continuum: [lista de paquetes de Anaconda](https://docs.continuum.io/anaconda/pkg-docs)

Servicios de aprendizaje de máquina en SQL Server 2017 también incluye el nuevo **revoscalepy** biblioteca de Python.

Esta biblioteca proporciona la funcionalidad equivalente a la de la **RevoScaleR** paquete para Microsoft R. En otras palabras, admite la creación de contextos de proceso remoto, así como un varios modelos de aprendizaje de máquina escalable, como **rxLinMod**. Para obtener más información sobre RevoScaleR, consulte [distribuida y la informática en paralelo con ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

El [microsoftml para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) paquete se instala como parte del aprendizaje automático de SQL Server al agregar Python a la instalación. Este paquete contiene muchos algoritmos que se han optimizado para la velocidad y la precisión, así como las transformaciones para trabajar con texto e imágenes en línea de aprendizaje de automático. Para obtener más información, consulte [con SQL Server en el paquete MicrosoftML](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package).

Microsoftml y revoscalepy están estrechamente Unidos; orígenes de datos usados en microsoftml se definen como objetos revoscalepy. Calcular las limitaciones de contexto de transferencia de revoscalepy a microsoftml. Es decir, toda la funcionalidad está disponible para las operaciones locales, pero cambia a un contexto de proceso remoto requiere RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Uso de Python en SQL Server

Importar la **revoscalepy** módulo a su código de Python y, a continuación, llamar a funciones desde el módulo, al igual que otras funciones de Python.

Datos de entrada para Python deben ser tabulares. Se deben devolver todos los resultados de Python en forma de un **pandas** trama de datos.

Puede ejecutar el código Python dentro de T-SQL, mediante la inserción de la secuencia de comandos en un procedimiento almacenado.

O bien, ejecute el código desde un IDE de Python local y tener el script que se ejecuta en el equipo de SQL Server, mediante la definición de un contexto de proceso remoto.

Puede trabajar con datos locales, obtener datos de SQL Server u otros orígenes de datos ODBC o usar el formato de archivo xdf. para intercambiar datos con otros orígenes, o con soluciones en R.

**Para obtener más información**

+ Funciones admitidas: [¿qué es revoscalepy](what-is-revoscalepy.md) 
+ Tipos de datos de Python admitidos: [bibliotecas de Python y tipos de datos](python-libraries-and-data-types.md)
+ Orígenes de datos admitidos: ODBC SQL Server, bases de datos y archivos xdf.
+ Admite contextos de proceso: local, o SQL Server

### <a name="licensing"></a>Licencias

Como parte de la instalación de servicios de aprendizaje de máquina con Python, debe dar su consentimiento a los términos de la licencia pública de GNU.

## <a name="see-also"></a>Vea también

[Bibliotecas de Python y tipos de datos](python-libraries-and-data-types.md)
