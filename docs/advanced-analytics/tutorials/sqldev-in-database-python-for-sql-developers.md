---
title: "En bases de datos análisis de Python para desarrolladores de SQL | Documentos de Microsoft"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 984ff8097b1f28cf11e28cc464c88dc3b9580a12
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="in-database-python-analytics-for-sql-developers"></a>En bases de datos análisis de Python para desarrolladores de SQL

El objetivo de este tutorial es proporcionar a los programadores SQL con experiencia práctica para crear un solución de SQL Server de aprendizaje automático. En este tutorial, aprenderá cómo incorporar Python a una aplicación mediante la adición de código Python a los procedimientos almacenados.

> [!NOTE]
> ¿Prefiere R? Vea [este tutorial](sqldev-in-database-r-for-sql-developers.md), lo que proporciona una solución similar pero usa R y puede ejecutarse eb en SQL Server 2016 o 2017 de SQL Server.

## <a name="overview"></a>Información general

El proceso de creación de una solución integral normalmente incluye la obtención y limpieza de los datos, la exploración de los datos y la ingeniería de características, el entrenamiento y la optimización del modelo, y por último la implementación del modelo en producción. Desarrollo y prueba del código real se realiza mejor usar un entorno de desarrollo dedicado, como estas herramientas Python:

+ PyCharm, un IDE popular
+ Spyder, que se incluye con [2017 de Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/) si instala el [cargas de trabajo de ciencia de datos](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)
+ [Extensiones de Python para Visual Studio](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio).

Una vez haya creado y probado la solución en el IDE, puede implementar el código de Python para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados en el entorno conocido de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

En este tutorial, supondremos que le ha proporcionado todo el código de Python necesario para la solución, y nos centraremos en generar e implementar la solución con SQL Server.

- [Paso 1: Descargar los datos de ejemplo](sqldev-py1-download-the-sample-data.md)

  Descargue el conjunto de datos de ejemplo y todos los archivos de script en un equipo local.

- [Paso 2: Importar datos a SQL Server mediante PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

  Ejecutar un script de PowerShell que crea una base de datos y una tabla en la instancia especificada y carga los datos de ejemplo a la tabla.

- [Paso 3: Explorar y visualizar los datos](sqldev-py3-explore-and-visualize-the-data.md)

  Realizar la exploración de datos básicos y visualización, por Python que realiza la llamada de [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados.

- [Paso 4: Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

  Cree nuevas características de datos mediante funciones personalizadas de SQL.
  
- [Paso 5: Entrenar y guardar un modelo con T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

   Crear y guardar el modelo de aprendizaje automático, que se usa Python en procedimientos almacenados.
  
-  [Paso 6: Hacer operativo el modelo](sqldev-py6-operationalize-the-model.md)

  Después de que el modelo se ha guardado en la base de datos, llame al modelo de predicción utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!NOTE]
> Se recomienda no usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para escribir o probar el código de Python. Si el código que incrusta en un procedimiento almacenado tiene algún problema, la información que se devuelve desde el procedimiento almacenado es normalmente inadecuada entender la causa del error.


### <a name="scenario"></a>Escenario

Este tutorial usa el conocido conjunto de datos NYC Taxi. Para realizar este tutorial rápido y sencillo, el muestreo de los datos. Con estos datos, se creará un modelo de clasificación binaria que predice si un viaje determinado es probable que obtenga una sugerencia o no, en función de las columnas como la hora del día, la distancia y la ubicación de recogida.

### <a name="requirements"></a>Requisitos

Este tutorial está destinado a usuarios que ya están familiarizados con las operaciones de base de datos fundamentales, como la creación de tablas y bases de datos, la importación de datos a tablas y la creación de consultas SQL.

Se proporciona todo el código Python. Un programador experimentado de SQL debe ser capaz de completar este tutorial con [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante la ejecución de los scripts de PowerShell proporcionados.

Antes de iniciar el tutorial, debe completar estos preparativos:

- Instalar una instancia de SQL Server 2017 con servicios de aprendizaje de máquina y Python habilitado (requiere la versión de CTP 2.0 o posterior).
- El inicio de sesión que use para este tutorial debe tener permisos para crear bases de datos y otros objetos, cargar datos, seleccionar datos y ejecutar procedimientos almacenados.

## <a name="next-step"></a>Paso siguiente

  [Paso 1: Descargar los datos de ejemplo](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>Vea también

[Los servicios con Python de aprendizaje automático](../python/sql-server-python-services.md)



