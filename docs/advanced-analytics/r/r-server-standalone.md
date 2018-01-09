---
title: R Server (independiente) | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 06/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
vms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: ca9e48f1-67b8-4905-9b78-56752d7a4e81
caps.latest.revision: "22"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: a7a7a83a1608a4505a3af0401dc8b6ac6f9c180a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="r-server-standalone"></a>R Server (Standalone)

En SQL Server 2016, Microsoft publicó **R Server (independiente)**, como parte de la plataforma para admitir el análisis de clase empresarial.  Microsoft R Server proporciona escalabilidad y seguridad para el lenguaje R y resuelve las limitaciones de memoria de código abierto R. Al igual que SQL Server R Services, Microsoft R Server (independiente) proporciona el procesamiento paralelo y fragmentado de datos, permitiendo a los usuarios de R usar datos mucho mayores que pueden caber en memoria.

En SQL Server 2017, se ha agregado compatibilidad para el lenguaje de Python, que le gusta una amplia compatibilidad con la Comunidad de máquina de aprendizaje en e incluye las populares bibliotecas para el análisis de texto y aprendizaje profundo.  Para reflejar este conjunto más amplio de idiomas, nos hemos también cambió su nombre a **aprendizaje de máquina de Microsoft Server (independiente)**.

## <a name="benefits-of-microsoft-r-server"></a>Ventajas de Microsoft R Server

Puede usar Microsoft R Server para la computación distribuida en varias plataformas. Cuando se instala desde el programa de instalación de SQL Server, aparece el servidor basado en Windows y todas las herramientas necesarias para los modelos de la publicación y distribución. Para obtener más información acerca de otras plataformas, consulte estos recursos en MSDN library:

+ [Introducción a Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)
+ [R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) (R Server para Windows)

También puede instalar Microsoft R Server para usar como un cliente de desarrollo, para obtener la RevoScaleR bibliotecas y las herramientas necesarias para crear soluciones de R que se pueden implementar en SQL Server.

## <a name="whats-new-in-microsoft-machine-learning-server"></a>Novedades de Microsoft Server de aprendizaje de máquina

Si instala Servicios de aprendizaje de máquina (independiente) utilizando el programa de instalación de SQL Server 2017, ahora tiene la opción para agregar el idioma de Python. Naturalmente, el lenguaje R sigue siendo una opción admitida y puede incluso instalar ambos lenguajes si lo desea.
 
En SQL Server de 2017 CTP 2.0, la instalación del servidor también incluye el paquete de mrsdeploy y otras utilidades que se usan para los modelos en marcha. Para obtener más información, consulte [puesta en marcha con mrsdeploy](../../advanced-analytics/operationalization-with-mrsdeploy.md).

Los usuarios empresariales de aprendizaje automático de SQL Server pueden usar a los instaladores que se pueden descargar para Microsoft R Server para actualizar sus componentes de R, en un proceso llamado enlace. Para obtener más información, consulte [SqlBindR de uso para la actualización y la instancia de SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

## <a name="get-microsoft-r-server-or-machine-learning-server-standalone"></a>Obtener Microsoft R Server o servidor de aprendizaje de máquina (independiente)

 Existen varias opciones para instalar Microsoft R Server:

+ Use el Asistente para la instalación de SQL Server

  [Crear un R Server independiente](../r/create-a-standalone-r-server.md)

  Ejecute el programa de instalación de SQL Server 2016 para instalar **Microsoft R Server (independiente)**. El lenguaje R se agrega de forma predeterminada.
  O bien, ejecute el programa de instalación de SQL Server 2017 para instalar **Server de aprendizaje de máquina (independiente)** y seleccione R, Python o ambos.

  > [!IMPORTANT]
  > La opción para instalar el servidor está en la **características compartidas** sección del programa de instalación. No instale ningún otro componente.
  >
  > Si es posible, no instale al servidor en un equipo donde se haya instalado SQL Server R Services o servicios de aprendizaje de máquina de SQL Server.

+ Usar opciones de línea de comandos para el programa de instalación de SQL Server

  [Instalar Microsoft R Server desde la línea de comandos](../r/install-microsoft-r-server-from-the-command-line.md)

  El programa de instalación de SQL Server es compatible con instalaciones desatendidas a través de un amplio conjunto de argumentos de línea de comandos.

+ Use el instalador independiente

  [Ejecutar Microsoft R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).

  Ahora puede usar a un nuevo instalador de Windows para configurar una nueva instancia de Microsoft R Server o servidor de aprendizaje de máquina de Microsoft.  Microsoft R Server (y aprendizaje de máquina de Microsoft Server) requieren un contrato Enterprise de SQL Server. Sin embargo, después de ejecutar al instalador independiente, se actualiza la directiva de soporte técnico para una instalación existente para usar la nueva directiva de ciclo de vida moderna. Esta opción de compatibilidad garantiza que las actualizaciones de componentes de aprendizaje de máquina se aplican con más frecuencia que serían al usar las versiones de servicio de SQL Server.

  
+ Actualizar una instancia de SQL Server

  [Uso de SqlBindR para actualizar una instancia de servicios de R](./use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).
  
  Puede usar al instalador independiente para actualizar una instancia de SQL Server 2016 R Services para usar la versión más reciente de R. Al ejecutar el programa de instalación, se aplicará la directiva de soporte técnico de ciclo de vida moderna para el servidor y los componentes de R obtendrá actualizaciones más frecuentes.
  
  > [! Tenga en cuenta} actualmente este método de actualización está disponible sólo para las instalaciones existentes de SQL Server 2016. Sin embargo, las actualizaciones se admitirá para SQL Server 2017 en el futuro.

## <a name="related-machine-learning-products"></a>Productos de aprendizaje de máquina relacionado

+ Máquinas virtuales de Azure con R Server

  [Aprovisionar una máquina Virtual de servidor de R](../../advanced-analytics/r-services/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure marketplace incluye varias imágenes de máquina virtual que incluyen R Server. Crear una nueva máquina virtual de servidor de R en Microsoft Azure es la manera más rápida de configurar un servidor para usar en el desarrollo e implementación de modelos de predicción. Imágenes de proceden con las características de ajuste de escala y uso compartido ya configurado, lo que facilita la que se va a incrustar el análisis de R en aplicaciones como integrar R con sistemas de back-end.

+ Máquina Virtual de ciencia de datos

  [Data Science Virtual Machine - Windows 2016 Preview](http://aka.ms/dsvm/win2016)

  La versión más reciente de la máquina Virtual de ciencia de datos incluye el servidor de R, SQL Server, y una matriz de las herramientas más populares para el aprendizaje automático, todos preinstalado y probado. Crear Jupyter blocs de notas, desarrollar soluciones de Julia y usar las bibliotecas de aprendizaje profundo basadas en la GPU como MXNet, CNTK y TensorFlow.

## <a name="resources"></a>Recursos

Ejemplos, tutoriales y obtener más información acerca de Microsoft R Server, vea [productos de Microsoft R](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started).

## <a name="see-also"></a>Vea también

 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)

