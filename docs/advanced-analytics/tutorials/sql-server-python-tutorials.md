---
title: Tutoriales de Python de SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 541675c22ddbe347f67119d8cba82f75955382e6
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48877989"
---
# <a name="sql-server-python-tutorials"></a>Tutoriales de Python de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se proporciona una lista de tutoriales y ejemplos que muestran el uso de Python con SQL Server 2017. A través de estos ejemplos y demostraciones, aprenderá lo siguiente:

+ Ejecución de Python desde T-SQL
+ ¿Cuáles son los contextos de cálculo locales y remotos, y cómo pueden ejecutar código de Python con el equipo de SQL Server
+ Cómo ajustar el código de Python en un procedimiento almacenado
+ Optimizar el código de Python para un entorno de producción de SQL
+ Escenarios del mundo real para la incrustación en aplicaciones de aprendizaje automático

Para obtener información sobre los requisitos y el programa de instalación, consulte [requisitos previos](#bkmk_Prerequisites).

## <a name="bkmk_pythontutorials"></a>Tutoriales de Python

+ [Ejecutar Python en T-SQL](run-python-using-t-sql.md)

   Obtenga información sobre los conceptos básicos de cómo llamar a Python en T-SQL, mediante el mecanismo de extensibilidad introducidas por primera vez en SQL Server 2016.

+ [Crear un modelo de machine learning en Python mediante revoscalepy](use-python-revoscalepy-to-create-model.md)

   En esta lección se muestra cómo ejecutar el código desde un terminal de Python remoto, utilizando el contexto de proceso de SQL Server. Debe estar un poco familiarizado con los entornos y herramientas de Python. Código de ejemplo es que crea un modelo con **rxLinMod**, desde el nuevo **revoscalepy** biblioteca. 

+ [Análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)

    En este tutorial de extremo a extremo muestra el proceso de creación de una solución completa de Python mediante procedimientos almacenado de Transact-SQL. Se incluye todo el código Python.


## <a name="python-samples"></a>Ejemplos de Python

Estos ejemplos y demostraciones proporcionadas por el equipo de desarrollo de SQL Server resaltan formas en que puede usar análisis insertados en aplicaciones del mundo real.

+ [Crear un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Obtenga información sobre cómo una empresa de alquiler de esquís puede usar el aprendizaje automático para predecir alquileres futuros, que permite el plan de negocio y personal para satisfacer la demanda futura.

  > [!TIP]
  > ¡Ahora incluye la puntuación nativa de modelos de Python!

+ [Realizar el cliente agrupación en clústeres con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Obtenga información sobre cómo usar el algoritmo de Kmeans para realizar una agrupación en clústeres no supervisado de los clientes.

## <a name="bkmk_Prerequisites"></a>Requisitos previos

Para utilizar estos tutoriales, debe tener SQL Server 2017, y debe instalar explícitamente y, a continuación, habilitar la característica, Machine Learning Services (In-Database). 

SQL Server 2017 admite los lenguajes R y Python, pero no está instalado o habilitado de forma predeterminada. La ejecución de Python requiere que esté habilitado el marco de extensibilidad y seleccionar Python como el idioma que desea instalar. 

### <a name="post-installation-configuration-tips"></a>Sugerencias de configuración posteriores a la instalación

Después de ejecutar el programa de instalación de SQL Server, es posible que necesite realizar algunos pasos adicionales para asegurarse de que se están comunicando Python y SQL Server:

+ Habilitar la característica de ejecución de scripts externos ejecutando `sp_configure 'external scripts enabled', 1`.
+ Reinicie el servidor. 
+ Abra el **servicios** panel para comprobar si ha iniciado el Launchpad. 
+ Asegúrese de que el servicio que llama el tiempo de ejecución externo tiene los permisos necesarios. Para obtener más información, consulte [habilita la autenticación implícita](../security/add-sqlrusergroup-to-database.md).
+ Abrir un puerto en el firewall para SQL Server y habilitar los protocolos de red necesarios.
+ Asegúrese de que la cuenta de usuario de Windows o inicio de sesión SQL tiene los permisos necesarios para conectarse al servidor, para leer los datos y para crear los objetos de base de datos requeridos por el ejemplo.

Consulte este artículo para algunos problemas comunes: [solución de problemas de servicios de Machine Learning](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>Administración de recursos

Puede instalar R y Python en el mismo equipo, pero ambos se ejecutan puede requerir muchos recursos. Si se producen errores de "memoria insuficiente", o si la ejecución de trabajos de machine learning es el que uso del servidor previsto de la entidad de seguridad, puede reducir la cantidad de memoria asignada al motor de base de datos. Para obtener más información, consulte [administración y supervisión de Python en SQL Server](../python/managing-and-monitoring-python-solutions.md).

## <a name="see-also"></a>Vea también

[Tutoriales de R para SQL Server](sql-server-r-tutorials.md)
