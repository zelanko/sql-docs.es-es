---
title: Interoperabilidad de Python | Documentos de Microsoft
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32762183ff5273998848978238788cc830319b91
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="python-interoperability"></a>Interoperabilidad de Python

En este tema se describe los componentes de Python que se instalan si se habilita la característica **Machine Learning Services (In-Database)** y seleccione Python como lenguaje.

> [!NOTE]
> Compatibilidad con Python es una característica de versión preliminar y está todavía en desarrollo.

## <a name="python-components"></a>Componentes de Python

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]no modifica los archivos ejecutables de Python. El tiempo de ejecución de Python se instala independientemente de las herramientas de SQL y se ejecuta fuera de la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] proceso.

La distribución que está asociada con un valor concreto [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia puede encontrarse en la carpeta asociada con la instancia.

Por ejemplo, si instala Servicios de aprendizaje de máquina con la opción de Python en la instancia predeterminada, mire debajo:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER`

Instalación de SQL Server de 2017 Machine Learning Services agrega la distribución de Anaconda de Python. En concreto, se usan los instaladores Anaconda 3, en función de la bifurcación Anaconda 4.3. El nivel de Python esperado para SQL Server 2017 es 3.5 de Python.

## <a name="new-in-this-release"></a>Novedades de esta versión

Para obtener una lista de paquetes admitidos por la distribución de Anaconda, vea el sitio de análisis de Continuum: [lista de paquetes de Anaconda](https://docs.continuum.io/anaconda/pkg-docs)

Servicios de aprendizaje de máquina en SQL Server 2017 también incluye el nuevo **revoscalepy** biblioteca de Python.

Esta biblioteca proporciona la funcionalidad equivalente a la de la **RevoScaleR** paquete para Microsoft R. En otras palabras, admite la creación de contextos de proceso remoto, así como un varios modelos de aprendizaje de máquina escalable, como **rxLinMod**. Para obtener más información sobre RevoScaleR, consulte [distribuida y la informática en paralelo con ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

Dado que admiten para Python es una característica de versión preliminar y está aún en desarrollo, el **revoscalepy** biblioteca actualmente sólo incluye un subconjunto de las funciones de RevoScaleR. 

Pueden incluir las adiciones futuras el [Kit de herramientas de Microsoft cognitivos](https://www.microsoft.com/research/product/cognitive-toolkit/). Conocido anteriormente como CNTK, esta biblioteca admite una variedad de modelos de red neuronal, incluidas redes convolutional (CNN), redes periódicos (RNN) y redes de largo memoria término corto (LSTM).

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

[Tipos de datos y las bibliotecas de Python](python-libraries-and-data-types.md)

