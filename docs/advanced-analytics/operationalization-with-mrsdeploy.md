---
title: "Implementar y consumir análisis mediante mrsdeploy | Documentos de Microsoft"
ms.custom: 
ms.date: 08/20/2017
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
ms.openlocfilehash: a8b090a9d5a9ed0a9f63b8f666fa9985089305ed
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---

# <a name="deploy-and-consume-analytics-using-mrsdeploy"></a>Implementar y consumir análisis mediante mrsdeploy

Microsoft R Server incluye una característica de puesta en marcha, **mrsdeploy**, que es compatible con estas tareas:

+ Para publicar y administrar modelos de R y Python y código en el formulario de servicios web
+ Usar estos servicios dentro de las aplicaciones cliente

Este tema proporciona información acerca de cómo habilitar y configurar la característica.

Para obtener información general sobre escenarios compatibles con **mrsdeploy**, consulte [puesta en marcha con R Server](https://docs.microsoft.com/r-server/what-is-operationalization).

## <a name="using-mrsdeploy-for-operationalization"></a>Uso de mrsdeploy para puesta en marcha

La palabra *puesta en marcha* puede significar muchas cosas:

+ La capacidad de publicar modelos a un servicio web para su uso por aplicaciones
+ Soporte para la informática distribuida o escalable
+ Una vez desarrollar, implementar muchas veces
+ Puntuación rápida para ambos varias filas y la puntuación del lote

Si ha instalado servicios de aprendizaje de máquina con SQL Server, *puesta en marcha* consiste en ajustar el código de R o Python en un procedimiento almacenado. Cualquier aplicación, a continuación, puede llamar al procedimiento almacenado para volver a entrenar un modelo, generar puntuaciones o crear informes. También puede automatizar trabajos mediante mecanismos de programación existentes en SQL Server.

Sin embargo, Microsoft R Server proporciona un mecanismo diferente para la compatibilidad con la implementación, con los servicios web que admiten la publicación de trabajos de R y una utilidad administrativa para ejecutar los trabajos de R distribuidos. Microsoft R Server utiliza las funciones de la **mrsdeploy** paquete para establecer una sesión con nodos de proceso remoto y ejecutar código R en una aplicación de consola.

Esta característica de implementación de R Server ofrece estas ventajas:

+ Control de acceso basado en roles a los servicios web analíticos

    Determinar quién puede publicar, actualizar y eliminar sus propios servicios web, aquellos que también se puede actualizar y eliminar los servicios web publican por otros usuarios y a quién puede única lista y consumen servicios web.

+ La puntuación más rápido
  
  Puede usar en tiempo real de puntuación con un objeto de modelo de R admitido para mejorar la velocidad de las operaciones de puntuación.

+ Publicar código Python como un servicio web

  Para obtener ejemplos, vea [publicar y consumir código Python](./python/publish-consume-python-code.md).

+ Consumo de lote asincrónico

  Servicios Web que requieren datos de entrada de gran tamaño ahora pueden utilizarse de forma asincrónica a través de la ejecución por lotes.

+ Ajuste automático de una cuadrícula de nodos de web y de proceso

  Una plantilla de script se proporciona para permitirle crear fácilmente un conjunto de máquinas virtuales del servidor de R en Azure y, a continuación, configurarlos como una cuadrícula de análisis y ejecución remota en marcha. Esta cuadrícula se puede aumentarse o hacia abajo según el uso de CPU.

+ Ejecución remota asincrónica

    Ahora compatible con la **mrsdeploy** paquete de R. Para continuar trabajando en el entorno de desarrollo durante la ejecución de scripts remotos, ejecute el script de R asincrónicamente mediante el `async` parámetro. Esto es especialmente útil cuando se ejecutan scripts que comprenden largos tiempos de ejecución.

## <a name="requirements-and-configuration"></a>Requisitos y configuración

SQL Server de 2017 CTP 2.0 y versiones posterior incluye esta característica, que estaba disponible anteriormente sólo con el servidor de R y no se instala con SQL Server R Services. El **mrsdeploy** paquete está instalado en el equipo de SQL Server, si selecciona la opción para instalar **aprendizaje de máquina de Microsoft Server**, desde el **características compartidas** sección de instalación de SQL Server.

Normalmente, no se recomienda que instale el servidor de aprendizaje de máquina en el mismo equipo que ejecuta Servicios de aprendizaje de máquina de SQL Server. Se recomienda que instale **aprendizaje de máquina de Microsoft Server** en un equipo independiente de SQL Server y, a continuación, configure las características de puesta en marcha en ese equipo.

Sin embargo, si necesita instalarlas juntas, siga estos pasos adicionales para configurar correctamente el servicio.

1. Instalar DotNetCore 1.1

    Si no se instaló .NET Core como parte de SQL Server, debe instalarlo antes de comenzar la instalación del servidor de R.

2. Instalar servidor de aprendizaje de automático de Microsoft.

3. Después de completar el programa de instalación de **aprendizaje de máquina de Microsoft Server**, manualmente agregar la siguiente clave del registro para **mrsdeploy**, que especifica la carpeta base para los archivos R_SERVER. 

    + Cree una nueva clave del registro`H_KEY_LOCAL_MACHINE\SOFTWARE\R Server\Path`
    + Establezca el valor de la clave `"C:\Program Files\Microsoft SQL Server\140\R_SERVER"`.

4. Cuando haya finalizado, abra el [administrador utilidad](https://docs.microsoft.com/r-server/operationalize/configure-use-admin-utility).

5. Continuar configurando la **mrsdeploy** servicio tal y como se describe aquí: [configuración para administradores](https://docs.microsoft.com/r-server/operationalize/configure-start-for-administrators)

6. Para obtener más información, consulte [mrsdeploy funciones](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package).

