---
title: Tutoriales de SQL Server Python | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 08/29/2017
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
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b891cda72d5a69aafe461918674218fd3279c423
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-python-tutorials"></a>Tutoriales de SQL Server Python

Este artículo proporciona una lista de tutoriales y ejemplos que muestran el uso de Python con SQL Server 2017. A través de estos ejemplos y demostraciones, obtendrá información sobre:

+ Ejecución de Python de T-SQL
+ ¿Cuáles son los contextos de proceso remotos y locales, y cómo pueden ejecutar código Python con el equipo de SQL Server
+ Cómo ajustar el código Python en un procedimiento almacenado
+ Optimizar el código de Python para un entorno de producción de SQL
+ Situaciones del mundo real para incrustar el aprendizaje automático de aplicaciones

Para obtener información sobre los requisitos y el programa de instalación, consulte [requisitos previos](#bkmk_Prerequisites).

## <a name="bkmk_pythontutorials"></a>Tutoriales de Python

+ [Ejecución de Python en T-SQL](run-python-using-t-sql.md)

   Obtenga información acerca de los conceptos básicos de cómo llamar a Python en T-SQL, mediante el mecanismo de extensibilidad que la primera en SQL Server 2016 aplicar.

+ [Crear un modelo en Python utilizando revoscalepy de aprendizaje automático](use-python-revoscalepy-to-create-model.md)

   Podrá crear un modelo con **rxLinMod**, desde el nuevo **revoscalepy** biblioteca. Aparecerá el código desde un terminal de Python remoto pero el modelado se llevará a cabo en el contexto de proceso de SQL Server.

+ [Crear un modelo de predicción con Python (GitHub)](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/python/getting-started/rental-prediction)

  Crear un modelo de aprendizaje automático para predecir la demanda de una empresa de alquiler de ski, y comenzar a ese modelo para la predicción de petición diarias mediante procedimientos almacenados. Se proporciona todo el código y datos.

+ [Análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)

  ¡NUEVO! Crear una solución completa de Python con los procedimientos almacenado de T-SQL. Se incluye todo el código Python.

+ [Implementar y utilizar un modelo de Python](..\python\publish-consume-python-code.md)

  Obtenga información acerca de cómo implementar un modelo de Python con la versión más reciente del servidor de aprendizaje de máquina de Microsoft.

## <a name="python-samples"></a>Ejemplos de Python

Estos ejemplos y demostraciones proporcionadas por el equipo de desarrollo de SQL Server resalte formas en que puede utilizar análisis incrustado en las aplicaciones reales.

+ [Crear un modelo de predicción mediante Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Obtenga información acerca de cómo una empresa de alquiler de ski puede usar el aprendizaje automático para predecir alquileres futuras, que le permite el plan de negocios y el personal para satisfacer la demanda futura.

+ [¡NUEVO! Realizar cliente agrupación en clústeres mediante Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Obtenga información acerca de cómo usar el algoritmo Kmeans para realizar la agrupación en clústeres supervisados de clientes.

## <a name="bkmk_Prerequisites"></a>Requisitos previos

Para utilizar estos tutoriales, debe tener instalado SQL Server 2017 Machine Learning Services (In-Database). Es compatible con SQL Server 2017 R o Python. Sin embargo, debe instalar el marco de extensibilidad que admite el aprendizaje automático y seleccione Python como el idioma que desea instalar. Puede instalar R y Python en el mismo equipo.

> [!NOTE]
>
> Compatibilidad con Python es una característica nueva de SQL Server 2017 y requiere la versión de CTP 2.0 o posterior. Aunque la característica está en versión preliminar y no se admite para los entornos de producción, le invitamos a probarlo y enviar comentarios.

**SQL Server 2017**

Después de ejecutar el programa de instalación de SQL Server, no olvide estos pasos importantes:

+ Habilitar la característica de ejecución de script externo mediante la ejecución`sp_configure 'external scripts enabled', 1`
+ Reiniciar el servidor
+ Asegúrese de que el servicio que llama el tiempo de ejecución externo tiene los permisos necesarios
+ Asegúrese de que la cuenta de usuario de Windows o inicio de sesión SQL tiene los permisos necesarios para conectarse al servidor, para leer los datos y para crear los objetos de base de datos requeridos por el ejemplo

Si experimenta problemas, consulte este artículo para algunos problemas comunes: [solución de problemas de servicios de aprendizaje de máquina](../machine-learning-troubleshooting-faq.md)

## <a name="see-also"></a>Vea también

[Tutoriales de R para SQL Server](sql-server-r-tutorials.md)

