---
title: Tutoriales de SQL Server Python | Documentos de Microsoft
titleSuffix: SQL Server
ms.custom: 
ms.date: 03/06/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: a9ba77cd6ec26e21136aa8ebfebfe67725b94ba2
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="sql-server-python-tutorials"></a>Tutoriales de SQL Server Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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

   Esta lección muestra cómo ejecutar código desde un terminal de Python remoto, utilizando el contexto de proceso de SQL Server. Debe estar un poco familiarizado con los entornos y herramientas de Python. Código de ejemplo es que crea un modelo con **rxLinMod**, desde el nuevo **revoscalepy** biblioteca. 

+ [Análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)

    Este tutorial de extremo a extremo muestra el proceso de creación de una solución completa de Python mediante procedimientos almacenado de T-SQL. Se incluye todo el código Python.

+ [Implementar y utilizar un modelo de Python](..\python\publish-consume-python-code.md)

  Aprenda a implementar un modelo de Python como un servicio web, utilizando la versión más reciente del servidor de aprendizaje de máquina de Microsoft.

## <a name="python-samples"></a>Ejemplos de Python

Estos ejemplos y demostraciones proporcionadas por el equipo de desarrollo de SQL Server resalte formas en que puede utilizar análisis incrustado en las aplicaciones reales.

+ [Crear un modelo de predicción mediante Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Obtenga información acerca de cómo una empresa de alquiler de ski puede usar el aprendizaje automático para predecir alquileres futuras, que le permite el plan de negocios y el personal para satisfacer la demanda futura.

  > [!TIP]
  > Ahora incluye la puntuación nativo de modelos de Python.

+ [Realizar cliente agrupación en clústeres mediante Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Obtenga información acerca de cómo usar el algoritmo Kmeans para realizar la agrupación en clústeres supervisados de clientes.

## <a name="bkmk_Prerequisites"></a>Requisitos previos

Para utilizar estos tutoriales, debe tener SQL Server 2017, y debe instalar explícitamente y, a continuación, habilita la característica, servicios de aprendizaje de máquina (In-Database). 

SQL Server 2017 admite idiomas de la R y Python, pero ninguna de ellas se instala o habilita de forma predeterminada. La ejecución de Python requiere que esté habilitado el marco de extensibilidad y que se selecciona Python como el idioma que desea instalar. 

### <a name="post-installation-configuration-tips"></a>Sugerencias de configuración posteriores a la instalación

Después de ejecutar el programa de instalación de SQL Server, deberá realizar algunos pasos adicionales para asegurarse de que se comunican Python y SQL Server:

+ Habilitar la característica de ejecución de script externo mediante la ejecución de `sp_configure 'external scripts enabled', 1`.
+ Reinicie el servidor. 
+ Abra la **servicios** panel para comprobar si se Launchpad ha iniciado. 
+ Asegúrese de que el servicio que llama el tiempo de ejecución externo tiene los permisos necesarios. Para obtener más información, consulte [habilitar la autenticación implícita](../r/add-sqlrusergroup-to-database.md).
+ Abrir un puerto en el firewall para SQL Server y habilitar protocolos de red necesarios.
+ Asegúrese de que la cuenta de usuario de Windows o inicio de sesión SQL tiene los permisos necesarios para conectarse al servidor, para leer los datos y para crear los objetos de base de datos requeridos por el ejemplo.

Consulte este artículo para algunos problemas comunes: [solución de problemas de servicios de aprendizaje de máquina](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>Administración de recursos

Puede instalar R y Python en el mismo equipo, pero ambos se ejecutan puede requerir muchos recursos. Si se producen errores de "memoria insuficiente", o si la ejecución de trabajos de aprendizaje de máquina es el que uso del servidor previsto de la entidad de seguridad, puede reducir la cantidad de memoria asignada al motor de base de datos. Para obtener más información, consulte [administración y supervisión de Python en SQL Server](../python/managing-and-monitoring-python-solutions.md).

## <a name="see-also"></a>Vea también

[Tutoriales de R para SQL Server](sql-server-r-tutorials.md)
