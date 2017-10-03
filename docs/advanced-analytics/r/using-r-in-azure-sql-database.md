---
title: Uso de R en la base de datos SQL Azure | Documentos de Microsoft
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 619921bbf00801fd5930a1c1b110e69a9fd05a81
ms.contentlocale: es-es
ms.lasthandoff: 09/30/2017

---
# <a name="using-r-in-azure-sql-database"></a>Uso de R en la base de datos SQL Azure

A partir de octubre de 2017, base de datos de SQL Azure admite la ejecución de R código de bases de datos mediante procedimientos almacenados, similares a los servicios de R en SQL Server 2016.

En este artículo se proporciona información general de la característica y describe las restricciones conocidas.

> [!NOTE]
> Esta versión es una versión de vista previa inicial y está pensada para las pruebas y exploración solo. Una versión de producción se publicarán unos instantes en 2018. La fecha de lanzamiento exacto y la compilación se basará en los comentarios del usuario. por lo que le recomendamos que pruebe la característica y háganoslo saber qué características son importantes. 
> 
> Para obtener información acerca de la programación de la versión, consulte el [blog de SQL Server](https://blogs.technet.microsoft.com/dataplatforminsider/) o [blog de Microsoft R Server](https://blogs.msdn.microsoft.com/rserver/).

## <a name="features"></a>Características

La versión preliminar proporciona la funcionalidad siguiente:

+ Llamar a R mediante procedimientos almacenados para facilitar la implementación de soluciones de aprendizaje automático
+ Obtener las puntuaciones de modelo mediante cualquier aplicación que pueda conectarse a la base de datos en la nube
+ Es compatible con la puntuación nativo mediante la función de PREDICCIÓN para puntuar rápida sin uso del runtime de R

Para conocer las restricciones específicas de la versión preliminar, consulte [restricciones y problemas conocidos](#bkmk_restrictions).

### <a name="components"></a>Components

La arquitectura global es similar de la máquina de SQL Server R Services.

**Seguridad**

+ El Launchpad de confianza de SQL Server administra la ejecución de trabajos de R y controla la duración de procesos. 

**Paquetes de R**

+ La versión de vista previa incluye Microsoft R Open 3.3.3 y Microsoft R Server versión 9.2. El [paquete RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) está preinstalado.

+ Algunos paquetes de R se han quitado o modificado para reducir el consumo en el entorno de Azure. Por ejemplo, **mrsdeploy** no se incluye en la base de datos de SQL Azure.

**Rendimiento**

+ Permite el entrenamiento y puntuación de cualquier modelo donde los datos caben en la memoria.  La cantidad de memoria disponible depende de la edición de la base de datos. 
+ Paralelismo trivial es compatible con la @parallel = 1 argumento, así como para la ejecución de script de R de transmisión por secuencias 
+ En la vista previa, limitada a un único script de R que se ejecute simultáneamente por base de datos.

**Idiomas**

El plan de futuras versiones incluye compatibilidad para paquetes adicionales y Python.

## <a name="restrictions"></a>Restricciones

Esta sección enumeran algunas limitaciones adicionales que se aplican a la versión de vista previa.

### <a name="upgrading-r-components-and-adding-packages-not-supported"></a>Actualizar componentes de R y la adición de paquetes no admitidos

La base de datos de SQL Azure es un servicio administrado, y los clientes no están pensados para administrar las actualizaciones de los componentes de R. Para obtener la versión preliminar, use los paquetes instalados disponibles.

Las actualizaciones a R y otro componentes de aprendizaje automático se publicará cuando estén disponibles.

### <a name="availability"></a>Disponibilidad

La capacidad de ejecutar R y otra máquina aprendizaje scripts de base de datos de SQL Azure es una característica de vista previa en el oeste región Ee.uu. Central solo. Expansión en otras regiones, como Europa occidental, está planeada para versiones posteriores.

Ejecutar código R en la base de datos de SQL Azure requiere suficiente almacenamiento y memoria. Actualmente se admiten los siguientes niveles de servicio de base de datos y los niveles de rendimiento:

+ Nivel de servicio Premium: P1, P2, P4, P6, P11, P15 
+ Nivel de servicio de RS de Premium: PRS1, PRS2, PRS4, PRS6 
+ Grupo elástico de Premium: 125 Edtu o superior 
+ Grupo de RS elástica Premium: 125 Edtu o superior 

### <a name="resource-management"></a>Administración de recursos

Esta versión no admite la capacidad para personalizar la instalación de R, o para supervisar el uso de scripts de R.

Por ejemplo, no se puede habilitar la ejecución de script de R solo en bases de datos específicas.

El sys.dm_db_resource_stats DMV, que se usa para supervisar el uso de CPU y memoria de los scripts de R, no está disponible en la versión preliminar.

### <a name="other-limitations"></a>Otras limitaciones

No se admite la funcionalidad siguiente: 

+ El paquete MicrosoftML no está disponible.
+ No se admiten características de administración de paquetes, como crear una biblioteca externa.
+ No puede usar la base de datos de SQL Azure como un contexto de proceso remoto al ejecutar las secuencias de comandos desde un cliente de R. Scripts de R se deben ejecutar utilizando el procedimiento almacenado sp_execute_external_script. Scripts que llama al procedimiento almacenado no pueden usar otros contextos de proceso.
+ No se puede ejecutar llamadas a funciones de recepción que requieren la ejecución en paralelo.
+ No se admiten conexiones de bucle invertido desde un script de R a SQL Server. En otras palabras, no se puede realizar llamadas externas desde el script de R a otro origen de datos ODBC.

## <a name="get-started"></a>Introducción

Este anuncio desde el equipo de desarrollo de SQL Server incluye ejemplos cortos que se pueden ejecutar en sus propias bases de datos de SQL Azure para experimentar con la creación de modelos de R y generar predicciones.

+ [Entrenar y modelos de puntuación en la base de datos SQL Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-preview-of-machine-learning-services-with-r-support-in-azure-sql-database/)

